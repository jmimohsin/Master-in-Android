**Webview Example**
===================

Android’s WebView allows you to open an own windows for viewing URL or custom
html markup page.  
In this tutorial, you will create two pages, a page with a single button, when
you clicked on it, it will navigate to another page and display URL “google.com”
in WebView component.

<br>**1. Android Layout Files**<br><br>
---------------------------------------

Create two Android layout files – “res/layout/main.xml” and
“res/layout/webview.xml“.  
File : res/layout/activity_main.xml

```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent" 
android:gravity="center">

<Button
android:id="@+id/buttonUrl"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Go to http://www.google.com" />
</RelativeLayout>
```

File : res/layout/webview_layout.xml – WebView example

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:orientation="vertical" >

<WebView xmlns:android="http://schemas.android.com/apk/res/android"
android:id="@+id/webView1"
android:layout_width="fill_parent"
android:layout_height="fill_parent" />
</LinearLayout>
```

 

**2. Activity**<br><br>
-----------------------

Two activity classes, an activity to display a button, another activity display
the WebView with predefined URL.  
File : MainActivity.java

```java
package rk.tutorial.webview.example;
import android.os.Bundle;
import android.app.Activity;
import android.content.Context;
import android.content.Intent;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.support.v4.app.NavUtils;
public class MainActivity extends Activity {
private Button button;
@Override
public void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.activity_main);
final Context context = this;
super.onCreate(savedInstanceState);
setContentView(R.layout.activity_main);
button = (Button) findViewById(R.id.buttonUrl);
button.setOnClickListener(new OnClickListener() {
@Override
public void onClick(View arg0) {
Intent intent = new Intent(context, WebViewActivity.class);
startActivity(intent);
}
});
}
}
```

File : WebViewActivity.java

```java
package rk.tutorial.webview.example;
import android.app.Activity;
import android.os.Bundle;
import android.webkit.WebView;
public class WebViewActivity extends Activity {
private WebView webView;
public void onCreate(Bundle savedInstanceState) {

super.onCreate(savedInstanceState);
setContentView(R.layout.webview_layout);
webView = (WebView) findViewById(R.id.webView1);
webView.getSettings().setJavaScriptEnabled(true);
webView.loadUrl("http://www.google.com");
}
}
```

 

**3. Android Manifest**<br><br>
-------------------------------

WebView required INTERNET permission, add below into AndroidManifest.xml.  
\<uses-permission android:name="android.permission.INTERNET" /\>  
File : AndroidManifest.xml – See full example.

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
package="rk.tutorial.webview.example"
android:versionCode="1"
android:versionName="1.0" >
<uses-sdk
android:minSdkVersion="8"
android:targetSdkVersion="15" />
<uses-permission android:name="android.permission.INTERNET"/>
<application
android:icon="@drawable/ic_launcher"
android:label="@string/app_name"
android:theme="@style/AppTheme" >

<activity
android:name=".MainActivity"
android:label="@string/app_name" >
<intent-filter>
<action android:name="android.intent.action.MAIN" />
<category android:name="android.intent.category.LAUNCHER" />
</intent-filter>
</activity>
<activity android:name=".WebViewActivity" android:label="@string/app_name"> </activity>
</application>
</manifest>
```

 

**4. Demo**
-----------

  
By default, just display a button.

![](file:///D:/Mohsin/assets/assets/img/webview.png)
