**Password field Example**
==========================

In Android, you can use “android.widget.EditText“, with inputType="textPassword"
to render a password component. In this tutorial, we show you how to use XML to
create a password field, label field and a normal button. When you click on the
button, the password value will be displayed as a floating message (toast
message).  
  


**1. Custom String** 
---------------------

  
Open “res/values/strings.xml” file, add some custom string for demonstration.  
File : res/values/strings.xml

```xml
<resources>
<string name="app_name">Password Field Example </string>
<string name="menu_settings">Settings </string>
<string name="title_activity_main">MainActivity </string>
<string name="lblPassword">Enter Your Password :</string>
<string name="btn_submit">Submit </string>
</resources>
```

**2. Password** 
----------------

  
Open “res/layout/ activity_main.xml” file, add a password component, EditText +
inputType="textPassword".  
File : res/layout/activity_main.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="fill_parent"
android:layout_height="fill_parent"
android:orientation="vertical" >

<TextView
android:id="@+id/lblPassword"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="@string/lblPassword"
android:textAppearance="?android:attr/textAppearanceLarge" />

<EditText
android:id="@+id/txtPassword"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:inputType="textPassword" >
<requestFocus />
</EditText>

<Button
android:id="@+id/btnSubmit"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="@string/btn_submit" />
</LinearLayout>
```

 

**3. Code Code** 
-----------------

  
Inside activity “onCreate()” method, attach a click listener on button, to
display the password value.  
File : MainActivity.java

```java
package rk.tutorial.password.field.example;
import android.app.Activity;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
public class MainActivity extends Activity {
private EditText password;
private Button btnSubmit;
@Override public void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.activity_main);
addListenerOnButton();
}
public void addListenerOnButton() {
password = (EditText) findViewById(R.id.txtPassword); 
btnSubmit = (Button) findViewById(R.id.btnSubmit);
btnSubmit.setOnClickListener(new OnClickListener() {
@Override
public void onClick(View v) {
Toast.makeText(MainActivity.this, password.getText(), Toast.LENGTH_SHORT).show();
}
});
}
}
```

 

**4. Demo** 
------------

  
Run the application.  
1. Result, password field is displayed.  


![](file:///D:/Mohsin/assets/assets/img/Password.png)
