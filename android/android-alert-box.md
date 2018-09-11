**Alert Box Example**
=====================

In this tutorial, we show you how to display an alert box in Android. See
flowing Steps :  
1. First, use the AlertDialog.Builder to create the alert box interface, like
title, message to display, buttons, and button onclick function  
2. Later attach above builder to AlertDialog and display it.  
3. Done.

<br>**1 Android Layout Files**
------------------------------

  
Simpel layout file, display a button on screen.  
File : res/layout/activity_main.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="fill_parent"
android:layout_height="fill_parent"
android:orientation="vertical"
android:gravity="center_horizontal" >

<Button 
android:layout_margin="20dip"
android:id="@+id/buttonAlert"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Show Alert Box" 
android:onClick="onClick"/>
</LinearLayout>
 
```

 

**2. Activity**
---------------

  
When user click on this button, display the alert box, with your pre-defined
alert dialog interface.  
File : MainActivity.java

```java
package rk.tutorial.alert.dialog.example;
import android.os.Bundle;
import android.app.Activity;
import android.app.AlertDialog;
import android.content.DialogInterface;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.support.v4.app.NavUtils;
public class MainActivity extends Activity {
@Override
public void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.activity_main);
}
public void onClick(View view){
AlertDialog.Builder alertDialogBuilder = new AlertDialog.Builder(MainActivity.this);
// set title
alertDialogBuilder.setTitle("Your Title");
// set dialog message
alertDialogBuilder .setMessage("Click yes to exit! No for Cancel dialog") .setCancelable(false) .setPositiveButton("Yes",new DialogInterface.OnClickListener() {
public void onClick(DialogInterface dialog,int id) {
// if this button is clicked, close
// current activity
MainActivity.this.finish();
}
})
.setNegativeButton("No",new DialogInterface.OnClickListener() {
public void onClick(DialogInterface dialog,int id) {
// if this button is clicked, just close
// the dialog box and do nothing
dialog.cancel();
}
});
// create alert dialog
AlertDialog alertDialog = alertDialogBuilder.create();
// show it
alertDialog.show();
}
}
```

 

**3.Demo**
----------

  
Display Screen

![](file:///D:/Mohsin/assets/assets/img/Alert.png)

![](file:///D:/Mohsin/assets/assets/img/Alert-box.png)

 
