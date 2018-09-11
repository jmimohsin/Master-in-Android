**Android Sending SMS**
=======================

There are following two ways to send SMS using Android device:

-   Using SmsManager to send SMS

-   Using Built-in Intent to send SMS

**Using SmsManager to send SMS**
--------------------------------

The SmsManager manages SMS operations such as sending data to the given mobile
device. You can create this object by calling the static method
SmsManager.getDefault() as follows:

```java
SmsManager smsManager = SmsManager.getDefault();
```

Once you have SmsManager object, you can use *sendDataMessage()* method to send
SMS at the specified mobile number as below:

```java
smsManager.sendTextMessage("phoneNo", null, "SMS text", null, null);
```

Apart from the above method, there are few other important functions available
in SmsManager class. These methods are listed below:

 

| **S.N.** | **Method & Description**                                                                                                                                                                                                                      |
|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1        | **ArrayList\<String\> divideMessage(String text)**                                                                                                                                                                                            |
|          | This method divides a message text into several fragments, none bigger than the maximum SMS message size.                                                                                                                                     |
| 2        | **static SmsManager getDefault()**                                                                                                                                                                                                            |
|          | This method is used to get the default instance of the SmsManager                                                                                                                                                                             |
| 3        | **void sendDataMessage(String destinationAddress, String scAddress, short destinationPort, byte[] data, PendingIntent sentIntent, PendingIntent deliveryIntent)**                                                                             |
|          | This method is used to send a data based SMS to a specific application port.                                                                                                                                                                  |
| 4        | **void sendMultipartTextMessage(String destinationAddress, String scAddress, ArrayList\<String\> parts, ArrayList\<PendingIntent\> sentIntents, ArrayList\<PendingIntent\> deliveryIntents)**                                                 |
|          | Send a multi-part text based SMS.                                                                                                                                                                                                             |
| 5        | **void sendTextMessage(String destinationAddress, String scAddress, String text, PendingIntent sentIntent, PendingIntent deliveryIntent)**                                                                                                    |
|          | Send a text based SMS.                                                                                                                                                                                                                        |

 

### **Example**

Following example shows you in practical how to use SmsManager object to send an
SMS to the given mobile number.

To experiment with this example, you will need actual Mobile device equipped
with latest Android OS, otherwise you will have to struggle with emulator which
may not work.

 

| **Step** | **Description**                                                                                                                                                                                                                                                                 |
|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1        | You will use Eclipse IDE to create an Android application and name it as *SendSMSDemo* under a package *com.example.sendsmsdemo*. While creating this project, make sure you *Target SDK* and *Compile With* at the latest version of Android SDK to use higher levels of APIs. |
| 2        | Modify *src/MainActivity.java* file and add required code to take care of sending email.                                                                                                                                                                                        |
| 3        | Modify layout XML file *res/layout/activity_main.xml* add any GUI component if required. I'm adding a simple GUI to take mobile number and SMS text to be sent and a simple button to send SMS.                                                                                 |
| 4        | Modify *res/values/strings.xml* to define required constant values                                                                                                                                                                                                              |
| 5        | Modify *AndroidManifest.xml* as shown below                                                                                                                                                                                                                                     |
| 6        | Run the application to launch Android emulator and verify the result of the changes done in the aplication.                                                                                                                                                                     |

 

Following is the content of the modified main activity file
**src/com.example.sendsmsdemo/MainActivity.java**.

 

```java
package com.example.sendsmsdemo;
 
import android.os.Bundle;
import android.app.Activity;
import android.telephony.SmsManager;
import android.util.Log;
import android.view.Menu;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
 
public class MainActivity extends Activity {
 
   Button sendBtn;
   EditText txtphoneNo;
   EditText txtMessage;
 
   @Override
   protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.activity_main);
 
      sendBtn = (Button) findViewById(R.id.btnSendSMS);
      txtphoneNo = (EditText) findViewById(R.id.editTextPhoneNo);
      txtMessage = (EditText) findViewById(R.id.editTextSMS);
 
      sendBtn.setOnClickListener(new View.OnClickListener() {
         public void onClick(View view) {
            sendSMSMessage();
         }
      });
 
   }
   protected void sendSMSMessage() {
      Log.i("Send SMS", "");
 
      String phoneNo = txtphoneNo.getText().toString();
      String message = txtMessage.getText().toString();
 
      try {
         SmsManager smsManager = SmsManager.getDefault();
         smsManager.sendTextMessage(phoneNo, null, message, null, null);
         Toast.makeText(getApplicationContext(), "SMS sent.",
         Toast.LENGTH_LONG).show();
      } catch (Exception e) {
         Toast.makeText(getApplicationContext(),
         "SMS faild, please try again.",
         Toast.LENGTH_LONG).show();
         e.printStackTrace();
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
 
   <TextView
   android:id="@+id/textViewPhoneNo"
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"
   android:text="@string/phone_label" />
 
   <EditText
   android:id="@+id/editTextPhoneNo"
   android:layout_width="fill_parent"
   android:layout_height="wrap_content"
   android:inputType="phone"/>
 
   <TextView
   android:id="@+id/textViewMessage"
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"
   android:text="@string/sms_label" />
 
   <EditText
   android:id="@+id/editTextSMS"
   android:layout_width="fill_parent"
   android:layout_height="wrap_content"
   android:inputType="textMultiLine"/>
 
   <Button android:id="@+id/btnSendSMS"
   android:layout_width="fill_parent"
   android:layout_height="wrap_content"
   android:text="@string/send_sms_label"/>
 
</LinearLayout>
```
Following will be the content of **res/values/strings.xml** to define two new
constants:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
 
    <string name="app_name">SendSMSDemo</string>
    <string name="action_settings">Settings</string>
    <string name="hello_world">Hello world!</string>
    <string name="phone_label">Enter Phone Number:</string>
    <string name="sms_label">Enter SMS Message:</string>
    <string name="send_sms_label">Send SMS</string>
   
</resources>
```

Let's try to run your **SendSMSDemo** application. I assume you have connected
your actual Android Mobile device with your computer. To run the app from
Eclipse, open one of your project's activity files and click Run icon from the
toolbar. Before starting your application, Eclipse will display following window
to select an option where you want to run your Android application.

Select your mobile device as an option and then check your mobile device which
will display following screen:

Now you can enter a desired mobile number and a text message to be sent on that
number. Finally click on **Sed SMS** button to send your SMS. Make sure your GSM
connection is working fine to deliver your SMS to its recipient.

You can take a number of SMS separated by comma and then inside your program you
will have to parse them into an array string and finally you can use a loop to
send message to all the given numbers. That's how you can write your own SMS
client. Next section will show you how to use existing SMS client to send SMS.

**Using Built-in Intent to send SMS**
-------------------------------------

You can use Android Intent to send SMS by calling built-in SMS functionality of
the Android. Following section explains different parts of our Intent object
required to send an SMS.

**Intent Object - Action to send SMS**
--------------------------------------

You will use **ACTION_VIEW** action to launch an SMS client installed on your
Android device. Following is simple syntax to create an intent with ACTION_VIEW
action

```xml
Intent smsIntent = new Intent(Intent.ACTION_VIEW);
```

**Intent Object - Data/Type to send SMS**
-----------------------------------------

To send an SMS you need to specify **smsto:** as URI using setData() method and
data type will be to **vnd.android-dir/mms-sms** using setType() method as
follows:

```xml
smsIntent.setData(Uri.parse("smsto:"));
smsIntent.setType("vnd.android-dir/mms-sms");
```

**Intent Object - Extra to send SMS**
-------------------------------------

Android has built-in support to add phone number and text message to send an SMS
as follows:

```xml
smsIntent.putExtra("address"  , new String("0123456789;3393993300"));
smsIntent.putExtra("sms_body"  , "Test SMS to Angilla");
```

### **Example**

Following example shows you in practical how to use Intent object to launch SMS
client to send an SMS to the given recipients.

To experiment with this example, you will need actual Mobile device equipped
with latest Android OS, otherwise you will have to struggle with emulator which
may not work.

 

| **Step**  | **Description**                                                                                                                                                                                                                                                                 |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1         | You will use Eclipse IDE to create an Android application and name it as *SendSMSDemo* under a package *com.example.sendsmsdemo*. While creating this project, make sure you *Target SDK* and *Compile With* at the latest version of Android SDK to use higher levels of APIs. |
| 2         | Modify *src/MainActivity.java* file and add required code to take care of sending SMS.                                                                                                                                                                                          |
| 3         | Modify layout XML file *res/layout/activity_main.xml* add any GUI component if required. I'm adding a simple button to launch SMS Client.                                                                                                                                       |
| 4         | Modify *res/values/strings.xml* to define required constant values                                                                                                                                                                                                              |
| 5         | Modify *AndroidManifest.xml* as shown below                                                                                                                                                                                                                                     |
| 6         | Run the application to launch Android emulator and verify the result of the changes done in the aplication.                                                                                                                                                                     |

 

Following is the content of the modified main activity file
**src/com.example.sendsmsdemo/MainActivity.java**.

```java
package com.example.sendsmsdemo;
 
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
 
      Button startBtn = (Button) findViewById(R.id.sendSMS);
      startBtn.setOnClickListener(new View.OnClickListener() {
         public void onClick(View view) {
         sendSMS();
      }
   });
 
   }
   protected void sendSMS() {
      Log.i("Send SMS", "");
 
      Intent smsIntent = new Intent(Intent.ACTION_VIEW);
      smsIntent.setData(Uri.parse("smsto:"));
      smsIntent.setType("vnd.android-dir/mms-sms");
 
      smsIntent.putExtra("address"  , new String ("0123456789"));
      smsIntent.putExtra("sms_body"  , "Test SMS to Angilla");
      try {
         startActivity(smsIntent);
         finish();
         Log.i("Finished sending SMS...", "");
      } catch (android.content.ActivityNotFoundException ex) {
         Toast.makeText(MainActivity.this,
         "SMS faild, please try again later.", Toast.LENGTH_SHORT).show();
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
 
   <Button android:id="@+id/sendSMS"
   android:layout_width="fill_parent"
   android:layout_height="wrap_content"
   android:text="@string/compose_sms"/>
   
</LinearLayout>
```

Following will be the content of **res/values/strings.xml** to define two new
constants:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
 
    <string name="app_name">SendSMSDemo</string>
    <string name="hello_world">Hello world!</string>
    <string name="action_settings">Settings</string>
    <string name="compose_sms">Compose SMS</string>
 
</resources>
```

Following is the default content of **AndroidManifest.xml**:

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.sendsmsdemo"
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
            android:name="com.example.sendsmsdemo.MainActivity"
            android:label="@string/app_name" >
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
 
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>
```

Let's try to run your **SendSMSDemo** application. I assume you have connected
your actual Android Mobile device with your computer. To run the app from
Eclipse, open one of your project's activity files and click Run icon from the
toolbar. Before starting your application, Eclipse will display following window
to select an option where you want to run your Android application.

Select your mobile device as an option and then check your mobile device which
will display following screen:

Now use **Compose SMS** button to launch Android built-in SMS clients which is
shown below

You can modify either of the given default fields and finally use send SMS
button (marked with red rectangle) to send your SMS to the mentioned recipient.
