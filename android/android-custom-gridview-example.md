**Custom gridview Example**
===========================

In this example, extend a BaseAdapter to display a group of image and text in
GridView layout.  


**2.1 Two Android Layout files**
--------------------------------

  
File – res/layout/activity_main.xml

```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent" >

<GridView
android:id="@+id/gridView1"
android:numColumns="auto_fit"
android:gravity="center"
android:columnWidth="100dp"
android:stretchMode="columnWidth"
android:layout_width="fill_parent"
android:layout_height="fill_parent" >
</GridView>
</RelativeLayout>
```

File – res/layout/custom_adapter_layout.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="match_parent"
android:layout_height="match_parent" >

<ImageView
android:id="@+id/grid_item_image"
android:layout_width="50px"
android:layout_height="50px"
android:layout_marginRight="10px"
android:src="@drawable/android_logo" >
</ImageView>

<TextView
android:id="@+id/grid_item_label"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="@+id/label"
android:layout_gravity="center"
android:layout_marginTop="5px"
android:textSize="15px" >
</TextView>
</LinearLayout>
```

 

**2.2 Main Activity**
---------------------

 

```java
package rk.tutorial.custom.adapter.example;
import android.app.Activity;
import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.AdapterView.OnItemClickListener;
import android.widget.GridView;
import android.widget.TextView;
import android.widget.Toast;
public class MainActivity extends Activity {
GridView gridView;
final String[] MOBILE_OS = new String[] { "Android", "Java", ".Net", "C++"};
@Override
public void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.activity_main);
gridView = (GridView) findViewById(R.id.gridView1);
gridView.setAdapter(new CustomAdapter(this, MOBILE_OS));
gridView.setOnItemClickListener(new OnItemClickListener() {
@Override
public void onItemClick(AdapterView parent, View v, int position, long id) {
Toast.makeText( getApplicationContext(), ((TextView) v.findViewById(R.id.grid_item_label)) .getText(), Toast.LENGTH_SHORT).show();
}
});
}
}
```

 

**2.3 Custom Activity**
-----------------------

 
```java
package rk.tutorial.custom.adapter.example;
import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseAdapter;
import android.widget.ImageView;
import android.widget.TextView;
public class CustomAdapter extends BaseAdapter {
private Context context;
private final String[] mobileValues;
public CustomAdapter(Context context, String[] mobileValues) {

this.context = context;
this.mobileValues = mobileValues;
}
public View getView(int position, View convertView, ViewGroup parent) {

LayoutInflater inflater = (LayoutInflater) context .getSystemService(Context.LAYOUT_INFLATER_SERVICE);
View gridView;
if (convertView == null) {
gridView = new View(context);
// get layout from mobile.xml
gridView = inflater.inflate(R.layout.custom_adapter_layout, null);
// set value into textview
TextView textView = (TextView) gridView .findViewById(R.id.grid_item_label);
textView.setText(mobileValues[position]);
// set image based on selected text
ImageView imageView = (ImageView) gridView .findViewById(R.id.grid_item_image);
String s = mobileValues[position];
if (s.equals(".Net")) {
imageView.setImageResource(R.drawable.dotnet_logo);
} else if (s.equals("Java")) {
imageView.setImageResource(R.drawable.java_logo);
} else if (s.equals("C++")) {
imageView.setImageResource(R.drawable.c_logo);
} else {
imageView.setImageResource(R.drawable.android_logo);
}
} else {
gridView = (View) convertView;
}
return gridView;
}
@Override
public int getCount() {
return mobileValues.length;
}
@Override
public Object getItem(int position) {
return null;
}
@Override
public long getItemId(int position) {

return 0;
}
}
```

**2.4 Demo**

![](file:///D:/Mohsin/assets/assets/img/Custom-gridview.png)
