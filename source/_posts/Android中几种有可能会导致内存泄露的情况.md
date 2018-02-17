---
title: Android中几种有可能会导致内存泄露的情况
date: 2015-08-14 13:20:20
tags:
---

1.Static静态成员导致的内存泄露

将占用大量内存空间的变量声明为static静态类型。当Activity被销毁的时候，由于静态成员的缘故，所占用的内存空间并没有得到及时的释放，最终导致内存泄漏。所以不要在静态空间中放太大的资源，如果一定要放，需要在结束的时候对其进行释放和清理。

```
public class MainActivity extends Activity {
    private static final int ARRAY_SIZE = 100;
    private static Drawable[] sTestBitmap = new Drawable[ARRAY_SIZE];
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        for (int i = 0 ; i < ARRAY_SIZE ; i++) {
            sTestBitmap[i] = getResources().getDrawable(R.drawable.test);
        }
        setContentView(R.layout.activity_main);
    }
    @Override
    protected void onDestroy() {
        super.onDestroy();
        /*for (int i = 0 ; i < ARRAY_SIZE ; i++) {
            sTestBitmap[i] = null;
        }
        sTestBitmap = null;
        System.gc();*/
    }
}

```

2.匿名内部类的使用 每一个匿名内部类都持有一个外部类的引用，当我们如果在一个匿名类中启动一个线程，那么它将一直持有外部类的引用，直到线程结束才能将内存空间释放。当我们在MainActivity中启动一个线程，虽然退出了该Activity，但是进程还在运行，MainActivity所占用的内存空间将得不到释放，导致最后的内存泄漏

```
public class MainActivity extends Activity {
    private Drawable mTestBitmap = null;
    private Thread mThread = null;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        mThread = new Thread(new Runnable() {
            @Override
            public void run() {
                while(true) {
                }
            }
        });
        mThread.start();
        mTestBitmap = getResources().getDrawable(R.drawable.test);
        setContentView(R.layout.activity_main);
    }
    @Override
    protected void onDestroy() {
        super.onDestroy();
        //TODO cancel Thread
    }
}

```

3.Context的滥用

```
private static Drawable sBackground;

    @Override  
    protected void onCreate(Bundle state){
        super.onCreate(state);
        TextView label = new TextView(this);  
        label.setText("Leaks are bad");  
        if (sBackground == null) {
            sBackground = getDrawable(R.drawable.large_bitmap);  
            }
        label.setBackgroundDrawable(sBackground);  
        setContentView(label);
    }
}

```

在这种情况下，Drawble持有Textiview的引用，TextView持有Activity的引用，即使Activity被销毁，内存仍然不会被释放。 若Context的引用超过其本身生命周期，也会导致内存泄漏，一般用getApplicationContext即可 * 使用Application这种Context类型 * 对Context的引用不要超过其自身生命周期 * 慎重使用Static关键字 * context里如果有限程，一定在onDestroy中结束掉 4.在Handler中遇到的问题 当使用内部类创建Handler的时候，Handler会持有一个外部Activity的引用。当Handler中的线程在执行的时候，Activity被GC，这时该线程持有Handler的引用，Handler含有Activity的引用，导致该Activity无法被回收，导致内存泄漏 解决办法： 1.通过程序逻辑来判断，在关闭Activity的同时停止线程，Activity就可以正常在合适的时候被回收。如果Handler是被delay的Message持有了引用，那么使用相应的Handler的removeCallbacks()方法，把消息对象从消息队列移除就行了 2.将Handler声明为静态类，不再持有外部类的引用，所以Activity可以被回收。

```
public class MainActivity extends Activity {    
    private final int MSG_DO_SOMETHING = 0;
    private SafeHandler mHandler = new SafeHandler(this);
    private TextView mTextView = null;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        mTextView = new TextView(this);
        Message.obtain(mHandler, MSG_DO_SOMETHING).sendToTarget();
        mHandler.sendMessageDelayed(Message.obtain(mHandler, MSG_DO_SOMETHING), 1000);
        setContentView(R.layout.activity_main);
    }
    static class SafeHandler extends Handler {
        WeakReference mActivityReference;
        SafeHandler(MainActivity activity) {
            mActivityReference= new WeakReference(activity);
        }
        @Override
        public void handleMessage(Message msg) {
            final MainActivity activity = mActivityReference.get();
            if (activity != null) {
                activity.mTextView.setTextColor(Color.WHITE);
            }
        }
    }
    @Override
    protected void onDestroy() {
        super.onDestroy();
        //删除所有Message
        mHandler.removeMessages(MSG_DO_SOMETHING, null);
        //删除Message.what==MSG_DO_SOMETHING的Message
        mHandler.removeMessages(MSG_DO_SOMETHING);
    }
}

```

总结：
不要让生命周期长于Activity的对象持有到Activity的引用
尽量使用Application的Context而不是Activity的Context
尽量不要在Activity中使用非静态内部类，因为非静态内部类会隐式持有外部类实例的引用（具体可以查看 细话Java：”失效”的private修饰符 了解）。如果使用静态内部类，将外部实例引用作为弱引用持有。
垃圾回收不能解决内存泄露，了解 Android中垃圾回收机制