**Custom Dialog box Example**
=============================

In this tutorial, we show you how to create a custom dialog in Android. See
following steps :  
1. Create a custom dialog layout (XML file).  
2. Attach the layout to Dialog.  
3. Display the Dialog.  
4. Done.

<br><br>**1 Android Layout Files**
----------------------------------

 

  
Two XML files, one for main screen, one for custom dialog.  
File : res/layout/activity_main.xm

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="fill_parent"
android:layout_height="fill_parent"
android:orientation="vertical" 
android:gravity="center_horizontal">

<Button
android:layout_margin="20dip"
android:id="@+id/buttonShowCustomDialog"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Show Custom Dialog" 
android:onClick="onClick"/>
</LinearLayout>
```


 

File : res/layout/custom_dialog.xml
-----------------------------------

 


```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="fill_parent"
android:layout_height="fill_parent" android:gravity="center_horizontal"
android:orientation="vertical">

<ImageView
android:id="@+id/image"
android:layout_margin="10dip"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:layout_marginRight="5dp" />

<TextView
android:id="@+id/text"
android:layout_width="fill_parent"
android:layout_height="wrap_content"
android:textColor="#FF000000"
android:gravity="center" 
android:layout_toRightOf="@+id/image"/>

<Button
android:id="@+id/dialogButtonOK"
android:layout_width="100px"
android:layout_height="wrap_content"
android:text=" Ok "
android:layout_marginTop="5dp"
android:layout_marginRight="5dp"
android:layout_below="@+id/image" />
</LinearLayout>
```


 

**2. Activity**
---------------

  
Read the comment and demo in next step, it should be self-explorary.  
File : MainActivity.java

 


```java
package rk.tutorial.custom.dialog.example;
import android.os.Bundle;
import android.app.Activity;
import android.app.Dialog;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.ImageView;
import android.widget.TextView;
import android.support.v4.app.NavUtils;
public class MainActivity extends Activity {
@Override
public void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.activity_main);
}
public void onClick(View v){
final Dialog dialog = new Dialog(MainActivity.this);
dialog.setContentView(R.layout.custom_dialog);
dialog.setTitle(" Your Title");
// set the custom dialog components - text, image and button
TextView text = (TextView) dialog.findViewById(R.id.text);
text.setText("Android custom dialog example!");
ImageView image = (ImageView) dialog.findViewById(R.id.image);
image.setImageResource(R.drawable.ic_launcher);
Button dialogButton = (Button) dialog.findViewById(R.id.dialogButtonOK);
// if button is clicked, close the custom dialog
dialogButton.setOnClickListener(new OnClickListener() {
@Override public void onClick(View v) {
dialog.dismiss();
}
});
dialog.show();
} 
}
```


 

**3. Demo**
-----------

 

 

![](file:///D:/Mohsin/assets/assets/img/Custom.png)

![](file:///D:/Mohsin/assets/assets/img/Custom-dialog.png)
