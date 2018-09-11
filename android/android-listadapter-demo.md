**ListAdapter Example**
=======================

In this example, we show you how to create 4 items in the ListView, and use a
custom “ArrayAdapter” to display different images base on the “item name” in the
list.  
  


**2.1 Images**<br><br>
----------------------

put 4 images for demonstration in drawable folder.  
  


**2.2 Android Layout file**  
File : res/layout/activity_main.xml


```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent" >

<ListView
android:id="@+id/prog_question"
android:layout_width="fill_parent"
android:layout_height="wrap_content" >
</ListView>
</RelativeLayout>
```


File: res/layout/custom_list_layout.xml


```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:padding="5dp" >

<ImageView
android:id="@+id/logo"
android:layout_width="120px"
android:layout_height="70px"
android:layout_marginLeft="5px"
android:layout_marginRight="20px"
android:layout_marginTop="5px"
android:src="@drawable/ic_launcher" >
</ImageView>

<TextView
android:id="@+id/label"
android:layout_width="fill_parent"
android:layout_height="wrap_content"
android:text="@+id/label"
android:gravity="center"
android:layout_gravity="center"
android:textSize="30px" >
</TextView>
</LinearLayout>
```


 

**2.3 Custom ArrayAdapter**
---------------------------

  
Create a class extends ArrayAdapter and customize the item display in the
getView() method.


```java
package rk.tutorial.custom.listview.example;
import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ArrayAdapter;
import android.widget.ImageView;
import android.widget.TextView;
public class CustomAdapter extends ArrayAdapter<String> {
private final Context context;
private final String[] values;
public CustomAdapter(Context context, String[] values) {
super(context, R.layout.custom_list_layout, values);
this.context = context;
this.values = values;
}
@Override
public View getView(int position, View convertView, ViewGroup parent) {

LayoutInflater inflater = (LayoutInflater) context .getSystemService(Context.LAYOUT_INFLATER_SERVICE);
View rowView = inflater.inflate(R.layout.custom_list_layout, parent, false);
TextView textView = (TextView) rowView.findViewById(R.id.label);
ImageView imageView = (ImageView) rowView.findViewById(R.id.logo);
textView.setText(values[position]);
// Change icon based on name
String s = values[position];
System.out.println(s);
if (s.equals(".Net")) {
imageView.setImageResource(R.drawable.dotnet_logo);
} else if (s.equals("Java")) {
imageView.setImageResource(R.drawable.java_logo);
} else if (s.equals("C++")) {
imageView.setImageResource(R.drawable.c_logo);
} else {
imageView.setImageResource(R.drawable.android_logo);
}
return rowView;
}
}
```


 

**2.4 ListView**
----------------

  
ListView, but use above custom adapter to display the list.


```java
package rk.tutorial.normal.listview.example;
import android.app.Activity;
import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.ListView;
import android.widget.Toast;
public class MainActivity extends Activity {
@Override
public void onCreate(Bundle savedInstanceState) {

super.onCreate(savedInstanceState);
setContentView(R.layout.activity_main);
final String[] QUESTION_LIST={"Android activity example","Android Password Field Example","Android Progress Bar Example","Android Alert Dialog Example","Android Custom Dialog Example","Android Normal ListView example","Custom array adapter to customize the item display in ListView","Android GridView Example"};
ArrayAdapter<String> adapter=new ArrayAdapter<String>(this, android.R.layout.simple_list_item_1, android.R.id.text1, QUESTION_LIST);
ListView question_listview=(ListView)findViewById(R.id.prog_question);
question_listview.setAdapter(adapter);
question_listview.setOnItemClickListener(new AdapterView.OnItemClickListener() {
@Override public void onItemClick(AdapterView arg0, View arg1, int arg2, long arg3) {
Toast.makeText(MainActivity.this, QUESTION_LIST[arg2], Toast.LENGTH_LONG).show();
}
});
}
}
```


**2.5 Demo**

![](file:///D:/Mohsin/assets/assets/img/listadapter.png)
