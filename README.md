实验内容
---
    1、本实验通过自定义WebView加载URL来验证隐式Intent的使用
    2、实验包含两个应用：
       第一个应用：获取URL地址并启动隐式Intent的调用
       第二个应用：自定义WebView来加载URL
    3、本项目为第二个应用MyBrowser——新建一个工程使用WebView来加载URL，即跳转之后，出现选择项，选择自定义的MyBrowser进行浏览
关键代码
---
1、ActionActivity.java
```
public class ActionActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_action);
        WebView webView=findViewById(R.id.webView);
        webView.loadUrl(String.valueOf(getIntent().getData()));
        webView.setWebViewClient(new WebViewClient(){
            @Override
            public boolean shouldOverrideUrlLoading(WebView view,String url){
                view.loadUrl(url);
                return true;
            }
        });
    }
}
```
2、activity_action.xml
```
    <WebView
        android:id="@+id/webView"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

    </WebView>
```
3、AndroidManifest.xml
```
    <activity android:name=".ActionActivity">
        <intent-filter>
            <action android:name="android.intent.action.VIEW"/>
            <category android:name="android.intent.category.DEFAULT"/>
            <category android:name="android.intent.category.BROWSABLE"/>
            <data android:scheme="http"/>
        </intent-filter>
    </activity>
```
结果截图
---
![image](https://github.com/YongxuanWu/MyBrowser/blob/master/app/src/main/res/pictures/Screenshot_20190504_184809.jpg)
![image](https://github.com/YongxuanWu/MyBrowser/blob/master/app/src/main/res/pictures/Screenshot_20190504_184832.jpg)
