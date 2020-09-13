# RemoteLogcatLibrary
An Android library that boots **an internal web server to display Android Logcat in your browser**. You will never need to connect your cable again to debug or view logs.

## How it works?
When you add this library to your Android application, it enables a web server to allow access to getting Android Logcat info in real-time. You only need run some browser and request a query to IP direction of your device (like http://192.168.0.128:8080). Note that is necesary share the same network. Once you get the fist connection to */log* path, automatically the content be reload frequently providing the latest changes. Remember that you can also filter the content using the search engine.

## How can you setup it?
You only need to follow these 3 steps:
 1) Add [this .AAR library](https://github.com/mipegir/RemoteLogcatLibrary/raw/master/downloads/remotelogcat_v1.1.aar) to your **app/libs** folder.
 2) Add these lines to the **app/build.gradle** file.
```java
    repositories {
        ...
        flatDir {
            dirs 'libs' 
        }
    }
    ...
    dependencies {
        compile fileTree(include: ['*.jar'], dir: 'libs')
        ...
        //RemoteLogcat
        compile(name: "remotelogcat_v1.1", ext: 'aar')
}
```
 3) Code this lines in your custom *Application class or Activity*.
```java
    @Override
    public void onCreate() {
        super.onCreate();

        if (BuildConfig.DEBUG) { //avoid execution on release, it is only for testing purpoise
            RemoteLogcatServer logcatServer 
                    = new RemoteLogcatServer(
                        8080,  //port to open connection
                        5000,  //page reload rate (ms)
                        getApplicationContext()
                     );
            logcatServer.startServer();
        }
    }
```

When you runs your APP, a default Android notification shows IP Address of your mobile phone to start conections. If you touch it, your browser opens welcome page to show tracked info from your Android Logcat.

### Custom bold hightlighting
```java
 private static final String TAG_REMOTE_LOGCAT_BOLD = "#RemoteLogcatBold#";
 Log.d("your_tag", TAG_REMOTE_LOGCAT_BOLD + "something to hightlight");
```

## 如何以模块的方式，加入到项目中？

> 相对依赖方式

* 1. ????
* 2. ????