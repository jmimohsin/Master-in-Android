# Android Intents and Filters

An Android **Intent** is an object carrying an _intent_ ie. message from one component to another component with-in the application or outside the application. The intents can communicate messages among any of the three core components of an application - activities, services, and broadcast receivers.

The intent itself, an Intent object, is a passive data structure holding an abstract description of an operation to be performed.

For example, let's assume that you have an Activity that needs to launch an email client and sends an email using your Android device. For this purpose, your Activity would send an ACTION_SEND along with appropriate **chooser**, to the Android Intent Resolver. The specified chooser gives the proper interface for the user to pick how to send your email data.

For example, assume that you have an Activity that needs to open URL in a web browser on your Android device. For this purpose, your Activity will send ACTION\_WEB\_SEARCH Intent to the Android Intent Resolver to open given URL in the web browser. The Intent Resolver parses through a list of Activities and chooses the one that would best match your Intent, in this case, the Web Browser Activity. The Intent Resolver then passes your web page to the web browser and starts the Web Browser Activity.

There are separate mechanisms for delivering intents to each type of component - activities, services, and broadcast receivers.


| S.N.        | Method & Description           | 
| ------------- |:-------------:| 
| 1      | **Context.startActivity()**<br>The Intent object is passed to this method to launch a new activity or get an existing activity to do something new. | 
| 2      | **Context.startService()**<br>The Intent object is passed to this method to initiate a service or deliver new instructions to an ongoing service.|
| 3      | **Context.sendBroadcast()**<br>The Intent object is passed to this method to deliver the message to all interested broadcast receivers. |

### Intent Objects

An Intent object is a bundle of information which is used by the component that receives the intent plus information used by the Android system.

An Intent object can contain the following components based on what it is communicating or going to perform:

### Action

This is mandatory part of the Intent object and is a string naming the action to be performed — or, in the case of broadcast intents, the action that took place and is being reported. The action largely determines how the rest of the intent object is structured . The Intent class defines a number of action constants corresponding to different intents. Here is a list of Android Intent Standard Actions

The action in an Intent object can be set by the setAction() method and read by getAction().

### Data

The URI of the data to be acted on and the MIME type of that data. For example, if the action field is ACTION_EDIT, the data field would contain the URI of the document to be displayed for editing.

The setData() method specifies data only as a URI, setType() specifies it only as a MIME type, and setDataAndType() specifies it as both a URI and a MIME type. The URI is read by getData() and the type by getType().

Some examples of action/data pairs are:

| S.N.| Action/Data Pair & Description| 
| ------------- |:-------------:| 
| 1      | **ACTION_VIEW content://contacts/people/1** <br> Display information about the person whose identifier is "1".| 
| 2      | **ACTION_DIAL content://contacts/people/1**<br>Display the phone dialer with the person filled in. | 
| 3      | **ACTION_VIEW tel:123**<br>Display the phone dialer with the given number filled in. | 
| 4      | **ACTION_DIAL tel:123**<br>Display the phone dialer with the given number filled in. | 
| 5      | **ACTION_EDIT content://contacts/people/1**<br>Edit information about the person whose identifier is "1". | 
| 6      | **ACTION_VIEW content://contacts/people/**<br>Display a list of people, which the user can browse through.| 
 


## Category

The category is an optional part of Intent object and it's a string containing additional information about the kind of component that should handle the intent. The addCategory() method places a category in an Intent object, removeCategory() deletes a category previously added, and getCategories() gets the set of all categories currently in the object. Here is a list of Android Intent Standard Categories.

You can check detail on Intent Filters in below section to understand how do we use categories to choose appropriate acivity coressponding to an Intent.

#### Extras

This will be in key-value pairs for additional information that should be delivered to the component handling the intent. The extras can be set and read using the putExtras() and getExtras() methods respectively. Here is a list of Android Intent Standard Extra Data

#### Flags

These flags are optional part of Intent object and instruct the Android system how to launch an activity, and how to treat it after it's launched etc.

#### Component Name

This optional field is an android **ComponentName** object representing either Activity, Service or BroadcastReceiver class. If it is set, the Intent object is delivered to an instance of the designated class otherwise Android uses other information in the Intent object to locate a suitable target.

The component name is set by setComponent(), setClass(), or setClassName() and read by getComponent().

## Types of Intents

There are following two types of intents supported by Android till version 4.1

**Explicit Intents**

These intents designate the target component by its name and they are typically used for application-internal messages - such as an activity starting a subordinate service or launching a sister activity. For example:

```java
// Explicit Intent by specifying its class name
Intent i = new Intent(this, TargetActivity.class);
i.putExtra("Key1", "ABC");
i.putExtra("Key2", "123");
 
// Starts TargetActivity
startActivity(i);
```

**Implicit Intents**

These intents do not name a target and the field for the component name is left blank. Implicit intents are often used to activate components in other applications. For example:

```java
// Implicit Intent by specifying a URI
Intent i = new Intent(Intent.ACTION_VIEW,
Uri.parse("http://www.example.com"));
 
// Starts Implicit Activity
startActivity(i);
```

The target component which receives the intent can use the **getExtras()** method to get the extra data sent by the source component. For example:

```java
// Get bundle object at appropriate place in your code
Bundle extras = getIntent().getExtras();
 
// Extract data using passed keys
String value1 = extras.getString("Key1");
String value2 = extras.getString("Key2");
```

**Example**

Following example shows the functionality of a Android Intent to launch various Android built-in applications.

| Step        | Description           | 
| ------------- |:-------------:| 
| 1      | You will use Eclipse IDE to create an Android application and name it as _IntentDemo_ under a package _com.example.intentdemo_. While creating this project, make sure you _Target SDK_ and _Compile With_ at the latest version of Android SDK to use higher levels of APIs. | 
| 2      | Modify _src__/MainActivity.java_ file and add the code to define two listeners corresponding two buttons ie. Start Browser and Start Phone. |  
| 3      | Modify layout XML file _res/layout/activity_main.xml_ to add three buttons in linear layout. | 
| 4      | Modify _res/values/strings.xml_ to define required constant values | 
| 5      | Run the application to launch Android emulator and verify the result of the changes done in the aplication. | 



Following is the content of the modified main activity file **src/com.example.intentdemo/MainActivity.java**.

```java
package com.example.intentdemo;
 
import android.net.Uri;
import android.os.Bundle;
import android.app.Activity;
import android.content.Intent;
import android.view.Menu;
import android.view.View;
import android.widget.Button;
 
public class MainActivity extends Activity {
 
   @Override
   protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.activity_main);
 
      Button startBrowser = (Button) findViewById(R.id.start_browser);
      startBrowser.setOnClickListener(new View.OnClickListener() {
         public void onClick(View view) {
            Intent i = new Intent(android.content.Intent.ACTION_VIEW,
            Uri.parse("http://www.example.com"));
            startActivity(i);
         }
      });
      Button startPhone = (Button) findViewById(R.id.start_phone);
      startPhone.setOnClickListener(new View.OnClickListener() {
         public void onClick(View view) {
            Intent i = new Intent(android.content.Intent.ACTION_VIEW,
            Uri.parse("tel:9510300000"));
            startActivity(i);
         }
      });
   } 
   @Override
   public boolean onCreateOptionsMenu(Menu menu) {
      // Inflate the menu; this adds items to the action
      // bar if it is present.
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
 
   <Button android:id="@+id/start_browser"
   android:layout_width="fill_parent"
   android:layout_height="wrap_content"
   android:text="@string/start_browser"/>
  
   <Button android:id="@+id/start_phone"
   android:layout_width="fill_parent"
   android:layout_height="wrap_content"
   android:text="@string/start_phone" />
 
</LinearLayout>
```

Following will be the content of **res/values/strings.xml** to define two new constants:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
 
    <string name="app_name">IntentDemo</string>
    <string name="action_settings">Settings</string>
    <string name="hello_world">Hello world!</string>
    <string name="start_browser">Start Browser</string>
    <string name="start_phone">Start Phone</string>
   
</resources>
```

Following is the default content of **AndroidManifest.xml**:

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.intentdemo"
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
            android:name="com.example.intentdemo.MainActivity"
            android:label="@string/app_name" >
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
 
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
 
</manifest>
```

Let's try to run your **IntentDemo** application. I assume you had created your **AVD** while doing environment setup. To run the app from Eclipse, open one of your project's activity files and click Run icon from the toolbar. Eclipse installs the app on your AVD and starts it and if everything is fine with your setup and application, it will display following Emulator window:

Now click on **Start Browser** button which will start a browser configured and display http://www.example.com as shown below:

Similar way Ou can launch phone interface using Start Phone button, which will allow you to dial already given phone number.

**Intent Filters**

You have seen how an Intent has been used to call an another activity. Android OS uses filters to pinpoint the set of Activities, Services, and Broadcast receivers that can handle the Intent with help of specified set of action, categories, data scheme associated with an Intent. You will use **<intent-filter>** element in the manifest file to list down actions, categories and data types associated with any activity, service, or broadcast receiver.

Following is an example of a part of **AndroidManifest.xml** file to specify an activity **com.example.intentdemo.CustomActivity** which can be invoked by either of the two mentioned actions, one category, and one data:

```xml
<activity android:name=".CustomActivity"
   android:label="@string/app_name">
   <intent-filter>
      <action android:name="android.intent.action.VIEW" />
      <action android:name="com.example.intentdemo.LAUNCH" />
      <category android:name="android.intent.category.DEFAULT" />
      <data android:scheme="http" />
   </intent-filter>
</activity>
```

Once this activity is defined along with above mentioned filters, other activities will be able to invoke this activity using either the **android.intent.action.VIEW**, or using the **com.example.intentdemo.LAUNCH** action provided their category is **android.intent.category.DEFAULT**.

The **&#60;data&#62;** element specifies the data type expected by the activity to be called and for above example our custom activity expects the data to start with the "http://"

There may be a situation that an intent can pass through the filters of more than one activity or service, the user may be asked which component to activate. An exception is raised if no target can be found.

There are following test Android checks before invoking an activity:

*   A filter &#60;intent-filter> may list more than one action as shown above but this list cannot be empty; a filter must contain at least one <action> element, otherwise it will block all intents. If more than one actions are mentioned then Android tries to match one of the mentioned actions before invoking the activity.
*   A filter &#60;intent-filter> may list zero, one or more than one categories. if there is no category mentioned then Android always pass this test but if more than one categories are mentioned then for an intent to pass the category test, every category in the Intent object must match a category in the filter.
*   Each &#60;data> element can specify a URI and a data type (MIME media type). There are separate attributes like **scheme, host, port**, and **path** for each part of the URI. An Intent object that contains both a URI and a data type passes the data type part of the test only if its type matches a type listed in the filter.

**Example**

Following example is a modification of the above example. Here we will see how Android resolves conflict if one intent is invoking two activities defined in, next how to invoke a custom activity using a filter and third one is an exception case if Android does not file appropriate activity defined for an intent.


| Step        | Description           | 
| ------------|:-------------:| 
| 1      | You will use Eclipse IDE to create an Android application and name it as _IntentDemo_ under a package _com.example.intentdemo_. While creating this project, make sure you _Target SDK_ and _Compile With_ at the latest version of Android SDK to use higher levels of APIs. | 
| 2      | Modify _src__/MainActivity.java_ file and add the code to define three listeners corresponding to three buttons defined in layout file. | 
| 3      | Add a new _src__/CustomActivity.java_ file to have one custom activity which will be invoked by different intents. |
| 4      | Modify layout XML file _res/layout/activity_main.xml_ to add three buttons in linear layout. |
| 5      | Add one layout XML file _res/layout/custom_view.xml_ to add a simple &#60;TextView> to show the passed data through intent. |
| 6      | Modify _res/values/strings.xml_ to define required constant values |
| 7      | Modify _AndroidManifest.xml_ to add &#60;intent-filter> to define rules for your intent to invoke custom activity. |
| 8      | Run the application to launch Android emulator and verify the result of the changes done in the aplication. | 



Following is the content of the modified main activity file **src/com.example.intentdemo/MainActivity.java**.

```java
package com.example.intentdemo;
 
import android.net.Uri;
import android.os.Bundle;
import android.app.Activity;
import android.content.Intent;
import android.view.Menu;
import android.view.View;
import android.widget.Button;
 
public class MainActivity extends Activity {
   
   @Override
   protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.activity_main);
 
      // First intent to use ACTION_VIEW action with correct data
      Button startBrowser_a = (Button) findViewById(R.id.start_browser_a);
      startBrowser_a.setOnClickListener(new View.OnClickListener() {
         public void onClick(View view) {
            Intent i = new Intent(android.content.Intent.ACTION_VIEW,
            Uri.parse("http://www.example.com"));
            startActivity(i);
         }
      });
 
      // Second intent to use LAUNCH action with correct data
      Button startBrowser_b = (Button) findViewById(R.id.start_browser_b);
      startBrowser_b.setOnClickListener(new View.OnClickListener() {
         public void onClick(View view) {
            Intent i = new Intent("com.example.intentdemo.LAUNCH",
            Uri.parse("http://www.example.com"));
            startActivity(i);
         }
      });
 
      // Third intent to use LAUNCH action with incorrect data
      Button startBrowser_c = (Button) findViewById(R.id.start_browser_c);
      startBrowser_c.setOnClickListener(new View.OnClickListener() {
         public void onClick(View view) {
            Intent i = new Intent("com.example.intentdemo.LAUNCH",
            Uri.parse("https://www.example.com"));
            startActivity(i);
         }
      });
 
   }
 
   @Override
   public boolean onCreateOptionsMenu(Menu menu) {
   // Inflate the menu; this adds items to the
   // action bar if it is present.
   getMenuInflater().inflate(R.menu.main, menu);
   return true;
   }
   
}
```

Following is the content of the modified main activity file **src/com.example.intentdemo/CustomActivity.java**.

```java
package com.example.intentdemo;
 
import android.app.Activity;
import android.net.Uri;
import android.os.Bundle;
import android.widget.TextView;
 
public class CustomActivity extends Activity {
   @Override
   public void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.custom_view);
 
      TextView label = (TextView) findViewById(R.id.show_data);
 
      Uri url = getIntent().getData();
      label.setText(url.toString());
   }
       
}
```

Following will be the content of **res/layout/activity_main.xml** file:

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
   android:layout_width="fill_parent"
   android:layout_height="fill_parent"
   android:orientation="vertical" >
 
   <Button android:id="@+id/start_browser_a"
   android:layout_width="fill_parent"
   android:layout_height="wrap_content"
   android:text="@string/start_browser_a"/>
 
   <Button android:id="@+id/start_browser_b"
   android:layout_width="fill_parent"
   android:layout_height="wrap_content"
   android:text="@string/start_browser_b"/>
  
   <Button android:id="@+id/start_browser_c"
   android:layout_width="fill_parent"
   android:layout_height="wrap_content"
   android:text="@string/start_browser_c"/>
 
</LinearLayout>
```

Following will be the content of **res/layout/custom_view.xml** file:

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"    >
   
   <TextView android:id="@+id/show_data"
   android:layout_width="fill_parent"
   android:layout_height="400dp"/>
  
</LinearLayout>
```

Following will be the content of **res/values/strings.xml** to define two new constants:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
 
    <string name="app_name">IntentDemo</string>
    <string name="action_settings">Settings</string>
    <string name="hello_world">Hello world!</string>
    <string name="start_browser_a">Start Browser with VIEW action</string>
    <string name="start_browser_b">Start Browser with LAUNCH action</string>
    <string name="start_browser_c">Exception Condition</string>
   
</resources>
```

Following is the default content of **AndroidManifest.xml**:

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.intentdemo"
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
            android:name="com.example.intentdemo.MainActivity"
            android:label="@string/app_name" >
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
 
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <activity android:name="com.example.intentdemo.CustomActivity"
            android:label="@string/app_name">
           <intent-filter>
              <action android:name="android.intent.action.VIEW" />
              <action android:name="com.example.intentdemo.LAUNCH" />
              <category android:name="android.intent.category.DEFAULT" />
              <data android:scheme="http" />
           </intent-filter>
        </activity>
    </application>
 
</manifest>
```

Let's try to run your **IntentDemo** application. I assume you had created your **AVD** while doing environment setup. To run the app from Eclipse, open one of your project's activity files and click Run icon from the toolbar. Eclipse installs the app on your AVD and starts it and if everything is fine with your setup and application, it will display following Emulator window:

Now let's start with first button "Stat Browser with VIEW Action". Here we have defined our custom activity with a filter "android.intent.action.VIEW", and there is already one default activity against VIEW action defined by Android which is launching web browser, so android displays following two options to select the activity you want to launch.

Now if yu select Browser, then Android will launch web browser and open example.com website but if you select IndentDemo option then Android will launch CustomActivity which does nothing but just capture passed data and displays in a text view as follows:

Now go back using back button and click on "Start Browser with LAUNCH Action" button, here Android applies filter to choose define activity and it simply launch your custom activity and again it displays following screen:

Again, go back using back button and click on "Exception Condition" button, here Android tries to find out a alid filter for the given intent but it does not find a valid activity defined because this time we have used data as **https** instead of **http** though we are giving a correct action, so Android raises an exception.
