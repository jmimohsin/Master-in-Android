**Activity Example**
====================

In Android, an activity is represent a single screen. Most applications have
multiple activities to represent different screens, for example, one activity to
display a list of the application settings, another activity to display the
application status.  
In this tutorial, we show you how to interact with activity, when a button is
clicked, navigate from current screen (current activity) to another screen
(another activity).

<br>**1. XML Layouts**
----------------------

  
  
Create following two XML layout files in “res/layout/” folder :  
1. res/layout/activity1_layout.xml – Represent screen 1  
2. res/layout/activity2_layout.xml – Represent screen 2  
File : res/layout/ activity1_layout.xml

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent" 
android:orientation="vertical"
android:gravity="center">

<TextView
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:layout_centerHorizontal="true"
android:layout_centerVertical="true"
android:padding="@dimen/padding_medium"
android:text="@string/activity1"
android:textAppearance="?android:attr/textAppearanceLarge"
tools:context=".Activity1" android:layout_margin="10dip"/>

<Button android:layout_width="fill_parent" 
android:layout_height="wrap_content"
android:padding="10dip"
android:text="@string/activity_button"
android:onClick="onClick"
android:layout_margin="10dip"/>
</LinearLayout>
```

File : res/layout/ activity2_layout.xml

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent" 
android:orientation="vertical" android:gravity="center">

<TextView
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:textAppearance="?android:attr/textAppearanceLarge"
android:padding="@dimen/padding_medium"
android:text="@string/activity2"
tools:context=".Activity1"
android:layout_margin="10dip"/>

<Button 
android:layout_width="fill_parent" 
android:layout_height="wrap_content"
android:padding="10dip"
android:text="@string/activity_button"
android:onClick="onClick"
android:layout_margin="10dip"/>
</LinearLayout>
```

 

**2. Activities** 
------------------

  
Create two activity classes :  
1. Activity1.java –\> main.xml  
2. Activity2.java –\> main2.xml To navigate from one screen to another screen,
use following code :  
Intent intent = new Intent(context, anotherActivity.class);  
startActivity(intent);  
File : Activity1.java

```java
package rk.tutorial.android.activity.examples;
import android.os.Bundle;
import android.app.Activity;
import android.content.Intent;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.support.v4.app.NavUtils;
public class Activity1 extends Activity {

@Override
public void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.activity1_layout);
}
public void onClick(View v){
Intent mIntent=new Intent(Activity1.this,Activity2.class);
startActivity(mIntent);
}
```

 

File : Activity2.java 
----------------------

 

```java
package rk.tutorial.android.activity.examples;
import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
public class Activity2 extends Activity {

@Override
public void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.activity2_layout);
}
public void onClick(View v){
Intent mIntent=new Intent(Activity2.this,Activity1.class);
startActivity(mIntent);
}
}
```

 

**3. AndroidManifest.xml** 
---------------------------

  
Declares above two activity classes in AndroidManifest.xml.  
File : AndroidManifest.xml

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
package="rk.tutorial.android.activity.examples"
android:versionCode="1"
android:versionName="1.0" >
<uses-sdk
android:minSdkVersion="8"
android:targetSdkVersion="15" />
<application
android:icon="@drawable/ic_launcher"
android:label="@string/app_name"
android:theme="@style/AppTheme" >

<activity
android:name=".Activity1"
android:label="@string/app_name" >
<intent-filter>
<action android:name="android.intent.action.MAIN" />
<category android:name="android.intent.category.LAUNCHER" />
</intent-filter>
</activity>

<activity android:name=".Activity2"
android:label="@string/app_name"></activity>
</application>
</manifest>
```

 

**4. Demo** 
------------

  
Run application.  
Activity1.java (activity1_layout.xml) screen is display.

![](file:///D:/Mohsin/assets/assets/img/Activity-one.png)

![](file:///D:/Mohsin/assets/assets/img/Activity-two.png)
