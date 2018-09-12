
# Android Sending Email

You have learnt Android Intent, which is an object carrying an intent ie. Message from one component to another component with-in the application or outside the application.

As such you do not need to develop your email client from scratch because they are already available like Gmail and K9mail. But you will need to send email from your Android application, where you will have to write an Activity that needs to launch an email client and sends an email using your Android device. For this purpose, your Activity will send an ACTION_SEND along with appropriate data load, to the Android Intent Resolver. The specified chooser gives the proper interface for the user to pick how to send your email data.

Following section explains different parts of our Intent object required to send an email.

## Intent Object - Action to send Email

You will use **ACTION_SEND** action to launch an email client installed on your Android device. Following is simple syntax to create an intent with ACTION_SEND action

```java
Intent emailIntent = new Intent(Intent.ACTION_SEND);
```

## Intent Object - Data/Type to send Email

To send an email you need to specify **mailto:** as URI using setData() method and data type will be to **text/plain** using setType() method as follows:

```java
emailIntent.setData(Uri.parse("mailto:"));
emailIntent.setType("text/plain");
```

## Intent Object - Extra to send Email

Android has built-in support to add TO, SUBJECT, CC, TEXT etc. fields which can be attached to the intent before sending the intent to a target email client. You can use following extra fields in your email:

| S.N.        | Extra Data & Description           | 
| ------------- |:------------- 
| 1      | **EXTRA_BCC**  <br>A String[] holding e-mail addresses that should be blind carbon copied. | 
| 2      | **EXTRA_CC** <br>A String[] holding e-mail addresses that should be carbon copied. |   
| 3      | **EXTRA_EMAIL**  <br>A String[] holding e-mail addresses that should be delivered to. | 
| 4      | **EXTRA_HTML_TEXT**  <br>A constant String that is associated with the Intent, used with ACTION_SEND to supply an alternative to EXTRA_TEXT as HTML formatted text. | 
| 5      | **EXTRA_SUBJECT**  <br>A constant string holding the desired subject line of a message. | 
| 6      | **EXTRA_TEXT** <br>A constant CharSequence that is associated with the Intent, used with ACTION_SEND to supply the literal data to be sent. | 
| 7      | **EXTRA_TITLE**  <br>A CharSequence dialog title to provide to the user when used with a ACTION_CHOOSER. | 



Here is an example showing you how to assign extra data to your intent:
```java
emailIntent.putExtra(Intent.EXTRA_EMAIL  , new String[]{"recipient@example.com"});
emailIntent.putExtra(Intent.EXTRA_SUBJECT, "subject of email");
emailIntent.putExtra(Intent.EXTRA_TEXT   , "body of email");
```

### Example

Following example shows you in practical how to use Intent object to launch Email client to send an Email to the given recipients.

To experiment with this example, you will need actual Mobile device equipped with latest Android OS, otherwise you will have to struggle with emulator which may not work. Second you will need to have an Email client like GMail or K9mail installed on your device.

| Step        | Description           | 
| ------------- |:-------------
| 1      | You will use Eclipse IDE to create an Android application and name it as _SendEmailDemo_ under a package _com.example.sendemaildemo_. While creating this project, make sure you _Target SDK_ and _Compile With_ at the latest version of Android SDK to use higher levels of APIs. | 
| 2      | Modify _src/MainActivity.java_ file and add required code to take care of sending email. | 
| 3      | Modify layout XML file _res/layout/activity_main.xml_ add any GUI component if required. I'm adding a simple button to launch Email Client. | 
| 4      | Modify _res/values/strings.xml_ to define required constant values | 
| 5      | Modify _AndroidManifest.xml_ as shown below |   
| 6      | Run the application to launch Android emulator and verify the result of the changes done in the aplication. |   



Following is the content of the modified main activity file **src/com.example.sendemaildemo/MainActivity.java**.

```java
package com.example.sendemaildemo;
 
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
 
      Button startBtn = (Button) findViewById(R.id.sendEmail);
      startBtn.setOnClickListener(new View.OnClickListener() {
         public void onClick(View view) {
         sendEmail();
      }
   });
 
   }
   protected void sendEmail() {
      Log.i("Send email", "");
 
      String[] TO = {"info@coders-hub.com"};
      String[] CC = {"jmi.mohsin@gmail.com"};
      Intent emailIntent = new Intent(Intent.ACTION_SEND);
      emailIntent.setData(Uri.parse("mailto:"));
      emailIntent.setType("text/plain");
 
 
      emailIntent.putExtra(Intent.EXTRA_EMAIL, TO);
      emailIntent.putExtra(Intent.EXTRA_CC, CC);
      emailIntent.putExtra(Intent.EXTRA_SUBJECT, "Your subject");
      emailIntent.putExtra(Intent.EXTRA_TEXT, "Email message goes here");
 
      try {
         startActivity(Intent.createChooser(emailIntent, "Send mail..."));
         finish();
         Log.i("Finished sending email...", "");
      } catch (android.content.ActivityNotFoundException ex) {
         Toast.makeText(MainActivity.this,
         "There is no email client installed.", Toast.LENGTH_SHORT).show();
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
 
   <Button android:id="@+id/sendEmail"
   android:layout_width="fill_parent"
   android:layout_height="wrap_content"
   android:text="@string/compose_email"/>
   
</LinearLayout>
```

Following will be the content of **res/values/strings.xml** to define two new constants:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
 
    <string name="app_name">SendEmailDemo</string>
    <string name="hello_world">Hello world!</string>
    <string name="action_settings">Settings</string>
    <string name="compose_email">Compose Email</string>
 
</resources>
```

Following is the default content of **AndroidManifest.xml**:

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.sendemaildemo"
    android:versionCode="1"
    android:versionName="1.0" >
 
    <uses-sdk
        android:minSdkVersion="8"
        android:targetSdkVersion="17" />
 
    <application
        android:allowBackup="true"
        android:icon="@drawable/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/AppTheme" >
        <activity
            android:name="com.example.sendemaildemo.MainActivity"
            android:label="@string/app_name" >
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
 
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>
```

Let's try to run your **SendEmailDemo** application. I assume you have connected your actual Android Mobile device with your computer. To run the app from Eclipse, open one of your project's activity files and click Run icon from the toolbar. Before starting your application, Eclipse will display following window to select an option where you want to run your Android application.

Select your mobile device as an option and then check your mobile device which will display following screen:

Now use **Compose Email** button to list down all the installed email clients. From the list, you can choose one f email clients to send your email. I'm going to use Gmail client to send my email which will have all the provided defaults fields available as shown below. Here **From:** will be default email ID you have registered for your Android device.

You can modify either of the given default fields and finally use send email button (marked with red rectangle) to send your email to the mentioned recipients.
