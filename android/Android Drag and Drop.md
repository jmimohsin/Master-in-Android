
# Android Drag and Drop

Android drag/drop framework allows your users to move data from one View to another View in the current layout using a graphical drag and drop gesture. The framework includes following three important components to support drag & drop functionality:

*   **Drag event class:**
*   **Drag listeners:**
*   **Helper methods and classes:**

**The Drag/Drop Process**

There are basically four steps or states in the drag and drop process:

*   **Started:** This event occurs when you start dragging an item in a layout, your application calls _startDrag()_ method to tell the system to start a drag. The arguments inside startDrag() method provide the data to be dragged, metadata for this data, and a callback for drawing the drag shadow.

The system first responds by calling back to your application to get a drag shadow. It then displays the drag shadow on the device.

Next, the system sends a drag event with action type _ACTION\_DRAG\_STARTED_ to the registered drag event listeners for all the View objects in the current layout.

To continue to receive drag events, including a possible drop event, a drag event listener must return **true**, If the drag event listener returns false, then it will not receive drag events for the current operation until the system sends a drag event with action type ACTION\_DRAG\_ENDED.

*   **Continuing:** The user continues the drag. System sends ACTION\_DRAG\_ENTERED action followed by ACTION\_DRAG\_LOCATION action to the registered drag event listener for the View where dragging point enters. The listener may choose to alter its View object's appearance in response to the event or can react by highlighting its View.

The drag event listener receives a ACTION\_DRAG\_EXITED action after the user has moved the drag shadow outside the bounding box of the View.

*   **Dropped:** The user releases the dragged item within the bounding box of a View. The system sends the View object's listener a drag event with action type ACTION_DROP.
*   **Ended:** Just after the action type ACTION\_DROP, the system sends out a drag event with action type ACTION\_DRAG_ENDED to indicate that the drag operation is over.

**The DragEvent Class**

The **DragEvent** represents an event that is sent out by the system at various times during a drag and drop operation. This class provides few Constants and important methods which we use during Drag/Drop process.

**Constants**

Following are all constants integers available as a part of DragEvent class.

| S.N.| **Constants & Description**|
| ------------- |:-------------:|
| 1    | **ACTION_DRAG_STARTED**<br> Signals the start of a drag and drop operation. |
| 2      | **ACTION_DRAG_ENTERED**<br>Signals to a View that the drag point has entered the bounding box of the View. |
| 3      | **ACTION_DRAG_LOCATION**<br>Sent to a View after ACTION_DRAG_ENTERED if the drag shadow is still within the View object's bounding box. |
| 4      | **ACTION_DRAG_EXITED**<br>Signals that the user has moved the drag shadow outside the bounding box of the View. |
| 5      | **ACTION_DROP**<br>Signals to a View that the user has released the drag shadow, and the drag point is within the bounding box of the View. |
| 6      | **ACTION_DRAG_ENDED**<br>Signals to a View that the drag and drop operation has concluded. |


**Methods**

Following are few important and most frequently used methods available as a part of DragEvent class.

| S.N.| Constants & Description|
| ------------- |:-------------:|
| 1    | **int** **getAction()**<br> Inspect the action value of this event.. |
| 2      | **ClipData** **getClipData()**<br>Returns the ClipData object sent to the system as part of the call to startDrag(). |
| 3      | **ClipDescription** **getClipDescription()**<br>Returns the ClipDescription object contained in the ClipData. |
| 4      | **boolean** **getResult()**<br>Returns an indication of the result of the drag and drop operation. |
| 5      | **float** **getX()**<br>Gets the X coordinate of the drag point. |
| 6      | **float** **getY()**<br>Gets the Y coordinate of the drag point. |
| 7      | **String toString()**<br>Returns a string representation of this DragEvent object. |



**Listening for Drag Event**

If you want any of your views within a Layout should respond Drag event then your view either implements **View.OnDragListener** or setup **onDragEvent(DragEvent)** callback method. When the system calls the method or listener, it passes to them a DragEvent object explained above. You can have both a listener and a callback method for View object. If this occurs, the system first calls the listener and then defined callback as long as listener returns true.

The combination of the _onDragEvent(DragEvent)_ method and _View.OnDragListener_ is analogous to the combination of the **onTouchEvent()** and **View.OnTouchListener** used with touch events in old versions of Android.

**Starting a Drag Event**

You start with creating a **ClipData** and **ClipData.Item** for the data being moved. As part of the _ClipData_ object, supply metadata that is stored in a **ClipDescription** object within the ClipData. For a drag and drop operation that does not represent data movement, you may want to use **null** instead of an actual object.

Next either you can extend extend **View.DragShadowBuilder** to create a drag shadow for dragging the view or simply you can use _View.DragShadowBuilder(View)_ to create a default drag shadow that's the same size as the View argument passed to it, with the touch point centered in the drag shadow.

**Example**

Following example shows the functionality of a simple Drag & Drop using a **View.setOnLongClickListener()** event listener along with **View.OnDragEventListener()**.


| Step| **Description**| 
| ------------- |:-------------:| 
| 1      | You will use Eclipse IDE to create an Android application and name it as _DragNDropDemo_ under a package _com.example.dragndropdemo_. While creating this project, make sure you _Target SDK_ and _Compile With_ at the latest version of Android SDK to use higher levels of APIs. |
| 2      | Modify _src/MainActivity.java_ file and add the code to define event listeners as well as a call back methods for the logo image used in the example. |
| 3      | Copy image logo.png in _res/drawable*_ folders. You can use images with different resolution in case you want to provide them for different devices. |
| 4      | Modify layout XML file _res/layout/activitymain.xml_ to define default view of the logo images. |
| 5      | Run the application to launch Android emulator and verify the result of the changes done in the aplication. | 

Following is the content of the modified main activity file **src/com.example.dragndropdemo/MainActivity.java**. This file can include each of the fundamental lifecycle methods.
```java
package com.example.dragndropdemo;
 
import android.os.Bundle;
import android.app.Activity;
import android.content.ClipData;
import android.content.ClipDescription;
import android.util.Log;
import android.view.DragEvent;
import android.view.View;
import android.view.View.DragShadowBuilder;
import android.view.View.OnDragListener;
import android.widget.*;
 
public class MainActivity extends Activity{
   ImageView ima;
   private static final String IMAGEVIEW_TAG = "Android Logo";
   String msg;
 
   private android.widget.RelativeLayout.LayoutParams layoutParams;
 
   @Override
   public void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.activity_main);
 
      ima = (ImageView)findViewById(R.id.iv_logo);
      // Sets the tag
      ima.setTag(IMAGEVIEW_TAG);
 
      ima.setOnLongClickListener(new View.OnLongClickListener() {
         @Override
         public boolean onLongClick(View v) {
            ClipData.Item item = new ClipData.Item((CharSequence)v.getTag());
 
            String\[\] mimeTypes = {ClipDescription.MIMETYPE\_TEXT\_PLAIN};
            ClipData dragData = new ClipData(v.getTag().toString(),
            mimeTypes, item);
 
            // Instantiates the drag shadow builder.
            View.DragShadowBuilder myShadow = new DragShadowBuilder(ima);
 
            // Starts the drag
            v.startDrag(dragData,  // the data to be dragged
            myShadow,  // the drag shadow builder
            null,      // no need to use local data
            0          // flags (not currently used, set to 0)
            );
            return true;
         }
      });
 
      // Create and set the drag event listener for the View
      ima.setOnDragListener( new OnDragListener(){
         @Override
         public boolean onDrag(View v,  DragEvent event){
         switch(event.getAction())                  
         {
            case DragEvent.ACTION\_DRAG\_STARTED:
               layoutParams = (RelativeLayout.LayoutParams)
               v.getLayoutParams();
               Log.d(msg, "Action is DragEvent.ACTION\_DRAG\_STARTED");
               // Do nothing
               break;
            case DragEvent.ACTION\_DRAG\_ENTERED:
               Log.d(msg, "Action is DragEvent.ACTION\_DRAG\_ENTERED");
               int x_cord = (int) event.getX();
               int y_cord = (int) event.getY(); 
               break;
            case DragEvent.ACTION\_DRAG\_EXITED :
               Log.d(msg, "Action is DragEvent.ACTION\_DRAG\_EXITED");
               x_cord = (int) event.getX();
               y_cord = (int) event.getY();
               layoutParams.leftMargin = x_cord;
               layoutParams.topMargin = y_cord;
               v.setLayoutParams(layoutParams);
               break;
            case DragEvent.ACTION\_DRAG\_LOCATION  :
               Log.d(msg, "Action is DragEvent.ACTION\_DRAG\_LOCATION");
               x_cord = (int) event.getX();
               y_cord = (int) event.getY();
               break;
            case DragEvent.ACTION\_DRAG\_ENDED   :
               Log.d(msg, "Action is DragEvent.ACTION\_DRAG\_ENDED");
               // Do nothing
               break;
            case DragEvent.ACTION_DROP:
               Log.d(msg, "ACTION_DROP event");
               // Do nothing
               break;
            default: break;
            }
            return true;
         }
      });
   }
}
```
Following will be the content of **res/layout/activity_main.xml** file:
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/container"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:orientation="vertical" >
       
    <ImageView
        android:id="@+id/iv_logo"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:src="@drawable/logo"
        android:contentDescription="@string/drag_drop"  />
          
</RelativeLayout>
```
Following will be the content of **res/values/strings.xml** to define two new constants:
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="app_name">DragNDropDemo</string>
    <string name="action_settings">Settings</string>
    <string name="hello_world">Hello world!</string>
    <string name="drag_drop">Click on the image to drag and drop</string>
</resources>

Following is the default content of **AndroidManifest.xml**:

<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.guidemo"
    android:versionCode="1"
    android:versionName="1.0" >
 
    <uses-sdk
        android:minSdkVersion="16"
        android:targetSdkVersion="17" />
 
    <application
        android:allowBackup="true"
        android:icon="@drawable/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/AppTheme" >
        <activity
            android:name="com.example.guidemo.MainActivity"
            android:label="@string/app_name" >
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
 
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
 
</manifest>
```
Let's try to run your **DragNDropDemo** application. I assume you had created your **AVD** while doing environment setup. To run the app from Eclipse, open one of your project's activity files and click Run icon from the toolbar. Eclipse installs the app on your AVD and starts it and if everything is fine with your setup and application, it will display following Emulator window:

Now do long click on the displayed android logo and you will see that logo image moves a little after 1 seconds long click from its place, its the time when you should start dragging the image. You can drag it around the screen and drop it at a new location.
