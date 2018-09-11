**Listview Example**
====================

In this example, we show you how to display a list of few android tutorial
question via ListView, it should be easy and self-explanatory.

<br>**1.1 Android Layout file**
-------------------------------

  
File : res/layout/activity_main.xml

```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent" >

<ListView
android:id="@+id/prog_question"
android:layout_width="fill_parent
android:layout_height="wrap_content" >
</ListView>
</RelativeLayout>
```

 

**1.2 Main Activity java Code**
-------------------------------

 

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

 

**1.3 Demo**
------------

 

![](file:///D:/Mohsin/assets/assets/img/listview_example.png)
