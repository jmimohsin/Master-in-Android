# Android Phone Calls

As such every Android Device especially Mobile phone is meant to provide a functionality to make a phone call but still you may need to write an application where you want to give an option to your user to make a call using a hard coded phone number.

This chapter lists down all the simple steps to create an application which can be used to make a Phone Call. You can use Android Intent to make phone call by calling built-in Phone Call functionality of the Android. Following section explains different parts of our Intent object required to make a call.

## Intent Object - Action to make Phone Call

You will use **ACTION_CALL** action to trigger built-in phone call functionality available in Android device. Following is simple syntax to create an intent with ACTION_CALL action

```java
Intent phoneIntent = new Intent(Intent.ACTION_CALL);
```

You can use **ACTION_DIAL** action instead of ACTION_CALL, in that case you will have option to modify hardcoded phone number before making a call instead of making a direct call.

## Intent Object - Data/Type to make Phone Call

To make a phone call at a given number 91-800-001-0101, you need to specify **tel:** as URI using setData() method as follows:

```java
phoneIntent.setData(Uri.parse("tel:91-800-001-0101"));
```

The interesting point is that, to make a phone call, you do not need to specify any extra data or data type.

### Example

Following example shows you in practical how to use Android Intent to make phone call to the given mobile number.

To experiment with this example, you will need actual Mobile device equipped with latest Android OS, otherwise you will have to struggle with emulator which may not work.

| Step        | Description           | 
| ------------- |:------------- 
| 1      | You will use Eclipse IDE to create an Android application and name it as _PhoneCallDemo_ under a package _com.example.phonecalldemo_. While creating this project, make sure you _Target SDK_ and _Compile With_ at the latest version of Android SDK to use higher levels of APIs. | 
| 2      | Modify _src/MainActivity.java_ file and add required code to take care of making a call. | 
| 3      | Modify layout XML file _res/layout/activity_main.xml_ add any GUI component if required. I'm adding a simple button to Call 91-800-001-0101 number |
| 4      | Modify _res/values/strings.xml_ to define required constant values |
| 5      | Modify _AndroidManifest.xml_ as shown below |
| 6      | Run the application to launch Android emulator and verify the result of the changes done in the aplication. |  



Following is the content of the modified main activity file **src/com.example.phonecalldemo/MainActivity.java**.

```java
package com.example.phonecalldemo;
 
import android.net.Uri;
import android.os.Bundle;
import android.app.Activity;
import android.content.Intent;
import android.util.Log;
import android.view.Menu;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;
 
public class MainActivity extends Activity {
 
   @Override
   protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.activity_main);
 
      Button startBtn = (Button) findViewById(R.id.makeCall);
      startBtn.setOnClickListener(new View.OnClickListener() {
         public void onClick(View view) {
         makeCall();
      }
   });
 
   }
   protected void makeCall() {
      Log.i("Make call", "");
 
      Intent phoneIntent = new Intent(Intent.ACTION_CALL);
      phoneIntent.setData(Uri.parse("tel:91-800-001-0101"));
 
      try {
         startActivity(phoneIntent);
         finish();
         Log.i("Finished making a call...", "");
      } catch (android.content.ActivityNotFoundException ex) {
         Toast.makeText(MainActivity.this,
         "Call faild, please try again later.", Toast.LENGTH_SHORT).show();
      }
   }
   @Override
   public boolean onCreateOptionsMenu(Menu menu) {
      // Inflate the menu; this adds items to the action bar if it is present.
      getMenuInflater().inflate(R.menu.main, menu);
      return true;
   }
}
```

Following will be the content of **res/layout/activity_main.xml** file:

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
   android:layout_width="fill_parent"
   android:layout_height="fill_parent"
   android:orientation="vertical" >
 
   <Button android:id="@+id/makeCall"
   android:layout_width="fill_parent"
   android:layout_height="wrap_content"
   android:text="@string/make_call"/>
   
</LinearLayout>
```

Following will be the content of **res/values/strings.xml** to define two new constants:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
 
    <string name="app_name">PhoneCallDemo</string>
    <string name="hello_world">Hello world!</string>
    <string name="action_settings">Settings</string>
    <string name="make_call">Call 91-800-001-0101</string>
 
</resources>
```
Following is the default content of **AndroidManifest.xml**:

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.phonecalldemo"
    android:versionCode="1"
    android:versionName="1.0" >
 
    <uses-sdk
        android:minSdkVersion="8"
        android:targetSdkVersion="17" />
   <uses-permission android:name="android.permission.CALL_PHONE" />
   <uses-permission android:name="android.permission.READ_PHONE_STATE" />
 
    <application
        android:allowBackup="true"
        android:icon="@drawable/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/AppTheme" >
        <activity
            android:name="com.example.phonecalldemo.MainActivity"
            android:label="@string/app_name" >
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
 
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>
```

Let's try to run your **PhoneCallDemo** application. I assume you have connected your actual Android Mobile device with your computer. To run the app from Eclipse, open one of your project's activity files and click Run icon from the toolbar. Before starting your application, Eclipse will display following window to select an option where you want to run your Android application.

Selct your mobile device as an option and then check your mobile device which will display following screen:

Now use **Call 91942-347-6192** button to make phone call.
