---
title: MVC与MVP模式的区别和联系
date: 2015-08-19 13:22:20
tags:
---

之前一直不清楚MVC模式和MVP模式的区别，今天查阅相关资料，找到了关于MVC和MVP在Android使用中的一些例子。
首先是MVC模式，这个模式应该已经用的很多了，MVC也就是Model、View、Controler（模型视图控制器模式）其中，Model层负责数据处理，view层负责界面交互的显示操作，而Controler控制器负责处理相关的应用逻辑。在Android应用的开发过程中，Model一般就是一些关于数据处理类似于网络通信、数据库访问等的一些执行方法等。Controler在Android中一般就是Activity、Service、ContentProvider等，负责处理一些关于逻辑上的问题。而View负责界面交互的显示，在Android中通常表现为XML文件。
MVC模式通常用于将视图与控制逻辑相分离，对应用进行解耦。但是解耦的效果并不是很好。
[![1426239008578777](http://wwdream-wordpress.stor.sinaapp.com/uploads/2015/08/1426239008578777.png)](http://wwdream-wordpress.stor.sinaapp.com/uploads/2015/08/1426239008578777.png)

 

从这张图中我们可以看到由于View可以与Model进行交互，直接获取Model的数据，而Model也可以直接对View进行操作（例如游标操作等），View不可避免的会含有一些逻辑信息，存在一定的耦合度。MVP就是为了解决这种耦合而存在的。Presenter的存在完美的解决了这种问题。Presenter负责视图层与模型层的交互，使得模型层不含有任何视图层的引用，Presenter层直接访问数据层获取信息，view层调用Presenter相应方法获取数据并显示，如果需要对界面显示进行回调的话，直接通过Presenter调用View相关方法进行回调。

对于MVP模式，我找了一个例子，可以更好的理解MVP模式。

首先是两个接口，分别为LoginVIew和LoginPresenter

LoginView：

```
public interface LoginView {
    public void showProgress();

    public void hideProgress();

    public void setUsernameError();

    public void setPasswordError();

    public void navigateToHome();
}

```

```
public interface LoginPresenter {
    public void validateCredentials(String username, String password);
}

```

OnLoginfinishedListener：

```
public interface OnLoginFinishedListener {

    public void onUsernameError();

    public void onPasswordError();

    public void onSuccess();
}

```

下面是这两个接口的实现：

```
public class LoginPresenterImpl implements LoginPresenter, OnLoginFinishedListener {

    private LoginView loginView;
    private LoginInteractor loginInteractor;

    public LoginPresenterImpl(LoginView loginView) {
        this.loginView = loginView;
        this.loginInteractor = new LoginInteractorImpl();
    }

    @Override public void validateCredentials(String username, String password) {
        loginView.showProgress();
        loginInteractor.login(username, password, this);
    }

    @Override public void onUsernameError() {
        loginView.setUsernameError();
        loginView.hideProgress();
    }

    @Override public void onPasswordError() {
        loginView.setPasswordError();
        loginView.hideProgress();
    }

    @Override public void onSuccess() {
        loginView.navigateToHome();
    }
}

```

```
public class LoginInteractorImpl implements LoginInteractor {
```

```
@Override
public void login(final String username, final String password, final OnLoginFinishedListener listener) {
    // Mock login. I'm creating a handler to delay the answer a couple of seconds
    new Handler().postDelayed(new Runnable() {
        @Override public void run() {
            boolean error = false;
            if (TextUtils.isEmpty(username)){
                listener.onUsernameError();
                error = true;
            }
            if (TextUtils.isEmpty(password)){
                listener.onPasswordError();
                error = true;
            }
            if (!error){
                listener.onSuccess();
            }
        }
    }, 2000);
}

```

}
LoginActivity：

```
public class LoginActivity extends Activity implements LoginView, View.OnClickListener {
```

```
private ProgressBar progressBar;
private EditText username;
private EditText password;
private LoginPresenter presenter;

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_login);

    progressBar = (ProgressBar) findViewById(R.id.progress);
    username = (EditText) findViewById(R.id.username);
    password = (EditText) findViewById(R.id.password);
    findViewById(R.id.button).setOnClickListener(this);

    presenter = new LoginPresenterImpl(this);
}

@Override public void showProgress() {
    progressBar.setVisibility(View.VISIBLE);
}

@Override public void hideProgress() {
    progressBar.setVisibility(View.GONE);
}

@Override public void setUsernameError() {
    username.setError(getString(R.string.username_error));
}

@Override public void setPasswordError() {
    password.setError(getString(R.string.password_error));
}

@Override public void navigateToHome() {
    startActivity(new Intent(this, MainActivity.class));
    finish();
}

@Override public void onClick(View v) {
    presenter.validateCredentials(username.getText().toString(), password.getText().toString());
}

```

}
我们可以看到，LoginActivity实现了LoginView接口，并且给出了其几个方法的实现。并且有一个LoginPresenter成员，负责处理与登陆有关的操作。例如OnResume就调用了presenter的OnResume方法。
在LoginPresenter接口的实现方法LoginPresenterImpl中，持有了MainActivity实现的LoginView方法，通过在操作该接口的一些方法实现对MainActivity进行回调。
总结一下，MVP模式由于没有视图层和模型层的耦合，可以完全的对视图进行解耦，通过相关的类进行操作，也很容易对其进行单元测试。但是由于MVP模式含有大量的接口，大量的使用可能会降低程序的可读性，让代码非常繁杂，所以可以只在部分代码中使用该模式，将模型层与视图层进行完全分离。

