# Android Notifications

Android **Toast** class provides a handy way to show users alerts but problem is that these alerts are not persistent which means alert flashes on the screen for a few seconds and then disappears.

For important messages to be given to the user, it is required to have more persistent method. A **notification** is a message you can display as an icon at the top of the device which we call notification bar or status bar.

To see the details of the notification, you will have to select the icon which will display notification drwer having detail about the notification. While working with emulator with virtual device, you will have to click and drag down the status bar to expand it which will give you detail as follows. This will be just **64 dp** tall and called normal view.

Above expanded form can have a **Big View** which will have additional detail about the notification? You can add upto six additional lines in the notification. The following screenshot shows such notification.

## Create and Send Notifications

You have simple way to create a notification. Follow the following steps in your application to create a notification:

### Step 1 - Create Notification Builder

As a first step is to create a notification builder using _NotificationCompat.Builder.build()_. You will use Notification Builder to set various Notification properties like its small and large icons, title, priority etc.
```java
NotificationCompat.Builder mBuilder = new NotificationCompat.Builder(this)
```

### Step 2 - Setting Notification Properties

Once you have **Builder** object, you can set its Notification properties using Builder object as per your requirement. But this is mandatory to set at least following:

- A small icon, set by **setSmallIcon()**
- A title, set by **setContentTitle()**
-   Detail text, set by **setContentText()**

```java
mBuilder.setSmallIcon(R.drawable.notification_icon);
mBuilder.setContentTitle("Notification Alert, Click Me!");
mBuilder.setContentText("Hi, This is Android Notification Detail!");
```
You have plenty of optional properties which you can set for your notification. To learn more about them, see the reference documentation for NotificationCompat.Builder.

### Step 3 - Attach Actions

This is an optional part and required if you want to attach an action with the notification. An action allows users to go directly from the notification to an **Activity** in your application, where they can look at one or more events or do further work.

The action is defined by a **PendingIntent** containing an **Intent** that starts an Activity in your application. To associate the PendingIntent with a gesture, call the appropriate method of _NotificationCompat.Builder_. For example, if you want to start Activity when the user clicks the notification text in the notification drawer, you add the PendingIntent by calling **setContentIntent()**.

A PendingIntent object helps you to perform an action on your application’s behalf, often at a later time, without caring of whether or not your application is running.

We take help of stack builder object which will contain an artificial back stack for the started Activity. This ensures that navigating backward from the Activity leads out of your application to the Home screen.

```java
Intent resultIntent = new Intent(this, ResultActivity.class);
TaskStackBuilder stackBuilder = TaskStackBuilder.create(this);
stackBuilder.addParentStack(ResultActivity.class);
 
// Adds the Intent that starts the Activity to the top of the stack
stackBuilder.addNextIntent(resultIntent);
PendingIntent resultPendingIntent =
        stackBuilder.getPendingIntent(
            0,
            PendingIntent.FLAG\_UPDATE\_CURRENT
        );
mBuilder.setContentIntent(resultPendingIntent);
````

### Step 4 - Issue the notification

Finally, you pass the Notification object to the system by calling NotificationManager.notify() to send your notification. Make sure you call **NotificationCompat.Builder.build()** method on builder object before notifying it. This method combines all of the options that have been set and return a new **Notification** object.

```java
NotificationManager mNotificationManager =
    (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);
   
// notificationID allows you to update the notification later on.
mNotificationManager.notify(notificationID, mBuilder.build());
```

## The NotificationCompat.Builder Class

The NotificationCompat.Builder class allows easier control over all the flags, as well as help constructing the typical notification layouts. Following are few important and most frequently used methods available as a part of NotificationCompat.Builder class.

| S.N.        | Constants & Description           | 
| ------------|:------------- 
| 1      | **Notification build()**<br>Combine all of the options that have been set and return a new Notification object. | 
| 2      | **NotificationCompat.Builder** **setAutoCancel (boolean autoCancel)**  <br>Setting this flag will make it so the notification is automatically canceled when the user clicks it in the panel. | 
| 3      | **NotificationCompat.Builder** **setContent (RemoteViews views)**  <br>Supply a custom RemoteViews to use instead of the standard one. | 
| 4      | **NotificationCompat.Builder** **setContentInfo (CharSequence info)**  <br>Set the large text at the right-hand side of the notification. | 
| 5      | **NotificationCompat.Builder** **setContentIntent (PendingIntent intent)**  <br>Supply a PendingIntent to send when the notification is clicked. | 
| 6      | **NotificationCompat.Builder** **setContentText (CharSequence text)** <br>Set the text (second row) of the notification, in a standard notification. | 
| 7      | **NotificationCompat.Builder** **setContentTitle (CharSequence title)**  <br>Set the text (first row) of the notification, in a standard notification. | 
| 8      | **NotificationCompat.Builder** **setDefaults (int defaults)**  <br>Set the default notification options that will be used. | 
| 9      | **NotificationCompat.Builder** **setLargeIcon (Bitmap icon)**  <br>Set the large icon that is shown in the ticker and notification. | 
| 10      | **NotificationCompat.Builder** **setNumber (int number)**  <br>Set the large number at the right-hand side of the notification. | 
| 11      | **NotificationCompat.Builder** **setOngoing (boolean ongoing)**  <br>Set whether this is an ongoing notification. | 
| 12      | **NotificationCompat.Builder** **setSmallIcon (int icon)**  <br>Set the small icon to use in the notification layouts. | 
| 13      | **NotificationCompat.Builder** **setStyle (NotificationCompat.Style style)**  <br>Add a rich notification style to be applied at build time. | 
| 14      | **NotificationCompat.Builder** **setTicker (CharSequence tickerText)**  <br>Set the text that is displayed in the status bar when the notification first arrives. | 
| 15      | **NotificationCompat.Builder** **setVibrate (long[] pattern)**  <br>Set the vibration pattern to use. | 
| 16      | **NotificationCompat.Builder** **setWhen (long when)**<br>Set the time that the event occurred. Notifications in the panel are sorted by this time. | 



### Example

Following example shows the functionality of a Android notification using a **NotificationCompat.Builder** Class which has been introduced in Android 4.1.

| Steps        | Description           | 
| ------------- |:------------- 
| 1      | You will use Eclipse IDE to create an Android application and name it as _NotificationDemo_ under a package _com.example.notificationdemo_. While creating this project, make sure you _Target SDK_ and _Compile With_ at the latest version of Android SDK to use higher levels of APIs. | 
| 2      | Modify _src__/MainActivity.java_ file and add the code to define three methods startNotification(), cancelNotification() and updateNotification() to cover maximum functionality related to Android notifications. | 
| 3      | Create a new Java file _src__/NotificationView.java_, which will be used to display new layout as a part of new activity which will be started when user will click any of the notifications |
| 4      | Copy image woman.png in _res/drawable-*_ folders and this image will be used as Notification icons. You can use images with different resolution in case you want to provide them for different devices. |
| 5      | Modify layout XML file _res/layout/activity_main.xml_ to add three buttons in linear layout. |
| 6      | Create a new layout XML file _res/layout/notification.xml_. This will be used as layout file for new activity which will start when user will click any of the notifications. |
| 7      | Modify _res/values/strings.xml_ to define required constant values |
| 8      | Run the application to launch Android emulator and verify the result of the changes done in the aplication. |

Following is the content of the modified main activity file **src/com.example.notificationdemo/MainActivity.java**. This file can include each of the fundamental lifecycle methods.

```java
package com.example.notificationdemo;
 
import android.os.Bundle;
import android.app.Activity;
import android.app.NotificationManager;
import android.app.PendingIntent;
import android.app.TaskStackBuilder;
import android.content.Context;
import android.content.Intent;
import android.support.v4.app.NotificationCompat;
import android.util.Log;
import android.view.View;
import android.widget.Button;
 
public class MainActivity extends Activity {
   private NotificationManager mNotificationManager;
   private int notificationID = 100;
   private int numMessages = 0;
 
   protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.activity_main);
 
      Button startBtn = (Button) findViewById(R.id.start);
      startBtn.setOnClickListener(new View.OnClickListener() {
         public void onClick(View view) {
            displayNotification();
         }
      });
 
      Button cancelBtn = (Button) findViewById(R.id.cancel);
      cancelBtn.setOnClickListener(new View.OnClickListener() {
         public void onClick(View view) {
            cancelNotification();
         }
      });
  
      Button updateBtn = (Button) findViewById(R.id.update);
      updateBtn.setOnClickListener(new View.OnClickListener() {
         public void onClick(View view) {
            updateNotification();
         }
      });
   }
   protected void displayNotification() {
      Log.i("Start", "notification");
 
      /* Invoking the default notification service */
      NotificationCompat.Builder  mBuilder =
      new NotificationCompat.Builder(this);  
 
      mBuilder.setContentTitle("New Message");
      mBuilder.setContentText("You've received new message.");
      mBuilder.setTicker("New Message Alert!");
      mBuilder.setSmallIcon(R.drawable.woman);
 
      /* Increase notification number every time a new notification arrives */
      mBuilder.setNumber(++numMessages);
     
      /* Creates an explicit intent for an Activity in your app */
      Intent resultIntent = new Intent(this, NotificationView.class);
 
      TaskStackBuilder stackBuilder = TaskStackBuilder.create(this);
      stackBuilder.addParentStack(NotificationView.class);
 
      /* Adds the Intent that starts the Activity to the top of the stack */
      stackBuilder.addNextIntent(resultIntent);
      PendingIntent resultPendingIntent =
         stackBuilder.getPendingIntent(
            0,
            PendingIntent.FLAG\_UPDATE\_CURRENT
         );
 
      mBuilder.setContentIntent(resultPendingIntent);
 
      mNotificationManager =
      (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);
 
      /* notificationID allows you to update the notification later on. */
      mNotificationManager.notify(notificationID, mBuilder.build());
   }
 
   protected void cancelNotification() {
      Log.i("Cancel", "notification");
      mNotificationManager.cancel(notificationID);
   }
 
   protected void updateNotification() {
      Log.i("Update", "notification");
 
      /* Invoking the default notification service */
      NotificationCompat.Builder  mBuilder =
      new NotificationCompat.Builder(this);  
 
      mBuilder.setContentTitle("Updated Message");
      mBuilder.setContentText("You've got updated message.");
      mBuilder.setTicker("Updated Message Alert!");
      mBuilder.setSmallIcon(R.drawable.woman);
 
     /* Increase notification number every time a new notification arrives */
      mBuilder.setNumber(++numMessages);
     
      /* Creates an explicit intent for an Activity in your app */
      Intent resultIntent = new Intent(this, NotificationView.class);
 
      TaskStackBuilder stackBuilder = TaskStackBuilder.create(this);
      stackBuilder.addParentStack(NotificationView.class);
 
      /* Adds the Intent that starts the Activity to the top of the stack */
      stackBuilder.addNextIntent(resultIntent);
      PendingIntent resultPendingIntent =
         stackBuilder.getPendingIntent(
            0,
            PendingIntent.FLAG\_UPDATE\_CURRENT
         );
 
      mBuilder.setContentIntent(resultPendingIntent);
 
      mNotificationManager =
      (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);
 
      /\* Update the existing notification using same notification ID */
      mNotificationManager.notify(notificationID, mBuilder.build());
   }
}
```

Following is the content of the modified main activity file **src/com.example.notificationdemo/NotificationView.java**.

```java
package com.example.notificationdemo;
 
import android.os.Bundle;
import android.app.Activity;
 
public class NotificationView extends Activity{
   @Override
   public void onCreate(Bundle savedInstanceState)
   {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.notification);
   }
 
}
```
Following will be the content of **res/layout/activity_main.xml** file:
```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
   android:layout_width="fill_parent"
   android:layout_height="fill_parent"
   android:orientation="vertical" >
 
   <Button android:id="@+id/start"
   android:layout_width="fill_parent"
   android:layout_height="wrap_content"
   android:text="@string/start_note"/>
 
 
   <Button android:id="@+id/cancel"
   android:layout_width="fill_parent"
   android:layout_height="wrap_content"
   android:text="@string/cancel_note" />
  
   <Button android:id="@+id/update"
   android:layout_width="fill_parent"
   android:layout_height="wrap_content"
   android:text="@string/update_note" />
 
</LinearLayout>
```

Following will be the content of **res/layout/notification.xml** file:
```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"    >
   <TextView
   android:layout_width="fill_parent"
   android:layout_height="400dp"
   android:text="Hi, Your Detailed notification view goes here...." />
</LinearLayout>
```
Following will be the content of **res/values/strings.xml** to define two new constants:

```java
<?xml version="1.0" encoding="utf-8"?>
<resources>
 
    <string name="app_name">NotificationDemo</string>
    <string name="action_settings">Settings</string>
    <string name="hello_world">Hello world!</string>
    <string name="start_note">Start Notification</string>
    <string name="cancel_note">Cancel Notification</string>
    <string name="update_note">Update Notification</string>
 
</resources>
```
Following is the default content of **AndroidManifest.xml**:

```java
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.notificationdemo"
    android:versionCode="1"
    android:versionName="1.0" >
 
    <uses-sdk
        android:minSdkVersion="17"
        android:targetSdkVersion="17" />
 
    <application
        android:allowBackup="true"
        android:icon="@drawable/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/AppTheme" >
        <activity
            android:name="com.example.notificationdemo.MainActivity"
            android:label="@string/app_name" >
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
 
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <activity android:name=".NotificationView"
             android:label="Details of notification"
             android:parentActivityName=".MainActivity">
       <meta-data
        android:name="android.support.PARENT_ACTIVITY"
        android:value=".MainActivity"/>
        </activity>
    </application>
 
</manifest>
```

Let's try to run your **NotificationDemo** application. I assume you had created your **AVD** while doing environment setup. To run the app from Eclipse, open one of your project's activity files and click Run icon from the toolbar. Eclipse installs the app on your AVD and starts it and if everything is fine with your setup and application, it will display following Emulator window:

Now click **Start Notification** button, you will see at the top a message "New Message Alert!" will display momentarily and after that you will have following screen having a small icon at the top left corner.

Now lets expand the view, long click on the small icon, after a second it will display date information and this is the time when you should drag status bar down without releasing mouse. You will see status bar will expand and you will get following screen:

Now let's try to click on the image icon, this will launch your new activity which you have set using intent and you will have following screen:

Next, you can click on "Detail of notification" and it will take you back to the main screen where you can try using **Update Notification** button which will update existing notification and number will increase by 1 but if you will send notification with new notification ID then it will keep adding in the stack and you see them separately listed on the screen.

**Big View Notification**

The following code snippet demonstrates how to alter the notification created in the previous snippet to use the Inbox big view style. I'm going to update displayNotification() modification method to show this functionality:

```java
protected void displayNotification() {
      Log.i("Start", "notification");
 
      /* Invoking the default notification service */
      NotificationCompat.Builder  mBuilder =
      new NotificationCompat.Builder(this);  
 
      mBuilder.setContentTitle("New Message");
      mBuilder.setContentText("You've received new message.");
      mBuilder.setTicker("New Message Alert!");
      mBuilder.setSmallIcon(R.drawable.woman);
 
      /* Increase notification number every time a new notification arrives */
      mBuilder.setNumber(++numMessages);
 
 
      /* Add Big View Specific Configuration */
      NotificationCompat.InboxStyle inboxStyle =
             new NotificationCompat.InboxStyle();
 
      String\[\] events = new String\[6\];
      events\[0\] = new String("This is first line....");
      events\[1\] = new String("This is second line...");
      events\[2\] = new String("This is third line...");
      events\[3\] = new String("This is 4th line...");
      events\[4\] = new String("This is 5th line...");
      events\[5\] = new String("This is 6th line...");
 
      // Sets a title for the Inbox style big view
      inboxStyle.setBigContentTitle("Big Title Details:");
      // Moves events into the big view
      for (int i=0; i < events.length; i++) {
 
         inboxStyle.addLine(events\[i\]);
      }
      mBuilder.setStyle(inboxStyle);
      
     
      /* Creates an explicit intent for an Activity in your app */
      Intent resultIntent = new Intent(this, NotificationView.class);
 
      TaskStackBuilder stackBuilder = TaskStackBuilder.create(this);
      stackBuilder.addParentStack(NotificationView.class);
 
      /* Adds the Intent that starts the Activity to the top of the stack */
      stackBuilder.addNextIntent(resultIntent);
      PendingIntent resultPendingIntent =
         stackBuilder.getPendingIntent(
            0,
            PendingIntent.FLAG\_UPDATE\_CURRENT
         );
 
      mBuilder.setContentIntent(resultPendingIntent);
 
      mNotificationManager =
      (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);
 
      /* notificationID allows you to update the notification later on. */
      mNotificationManager.notify(notificationID, mBuilder.build());
   }
```
Now you will try to run your application.
