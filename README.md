# RESQhive Android SDK

Simply saying, RESQhive is a cypto miner. The RESQhive JavaScript Miner lets developers embed a Monero miner directly into websites. There wasn't any solution for Android to mine Monero from apps, until [theapache64](https://github.com/theapache64/coin_hive_android_sdk) developed one. The RESQhive Android Miner is a hard fork of that work.

### Demo


<img src="https://raw.githubusercontent.com/resqs/resqhive_android_sdk/master/coinhive_example.gif" width="400">


### Installation

Install the dependency.

```groovy
compile 'com.theah64.coinhive:coinhive:1.2.2'
```



Add `INTERNET` permission

```xml
<uses-permission android:name="android.permission.INTERNET" />
```


Init in your application

```java
public class App extends Application {

    @Override
    public void onCreate() {
        super.onCreate();

        CoinHive.getInstance()
                .init("YOUR-SITE-KEY") // mandatory
                .setNumberOfThreads(4) // optional
                .setIsAutoThread(true) // optional
                .setThrottle(0.2) // optional
                .setLoggingEnabled(true) // To logcat mining status, false by default.
                .setForceASMJS(false); // optional

    }
}
```

Don't forget to add `App` class to your `manifest`.
Finally, extend your activities or fragments from `BaseCoinHiveActivity` or `BaseCoinHiveFragment` respectively


```java
public class MainActivity extends BaseCoinHiveActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        
        //Usual stuff
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);
        

    }

}
```

Done. Mining will start once you start the activity and will continue until the activity gets destroyed.
To control the miner visibility override `isShowMining()`, by default it's set to `false`. 

### Miner status

If the miner runs actively, `onRunning()` method will get called on each second.

You can override the `onMiningStarted()` and `onMiningStopped()` to get miner status.

```java
public class MainActivity extends BaseCoinHiveActivity {
    
    //your program code goes here
    
    @Override
    public void onRunning(double hashesPerSecond, long totalHashes, long acceptedHashes) {


    }

    @Override
    private void onMiningStarted() {


    }
    
    @Override
    private void onMiningStopped() {


    }

}
```

### Miner controls

To stop the miner, call `stopMining()`.

To start the miner, call `startMining()`.

NOTE: By default, miner starts automatically.


### Issue or Improvements

Use pull-requests to initiate discussions with RESQs Dev Team. 
OR
Shoot the original developer an e-mail to: theapache64@gmail.com :)

