**GridView Example**
====================

In Android, GridView let you arranges components in a two-dimensional scrolling
grid.  
Display characters from A to Z in GridView layout. Quite simple, it should be
sef-explanatory.  
  


**1.1 Android Layout file** – res/layout/activity_main.xml

```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent" >

<GridView xmlns:android="http://schemas.android.com/apk/res/android"
android:id="@+id/gridView1"
android:numColumns="auto_fit"
android:gravity="center"
android:columnWidth="50dp"
android:stretchMode="columnWidth"
android:layout_width="fill_parent"
android:layout_height="fill_parent" >
</GridView>
</RelativeLayout>
```


 

**1.2 MainActivity**
--------------------

 

```java
package rk.tutorial.gridview.example;
import android.os.Bundle;
import android.app.Activity;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.widget.AdapterView;
import android.widget.AdapterView.OnItemClickListener;
import android.widget.ArrayAdapter;
import android.widget.GridView;
import android.widget.TextView;
import android.widget.Toast;
import android.support.v4.app.NavUtils;
public class MainActivity extends Activity {
GridView gridView; static final String[] numbers = new String[] { 
"A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z"};
@Override
public void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.activity_main);
gridView = (GridView) findViewById(R.id.gridView1);
ArrayAdapter<String> adapter = new ArrayAdapter<String>(this, android.R.layout.simple_list_item_1, numbers);
gridView.setAdapter(adapter);
gridView.setOnItemClickListener(new OnItemClickListener() {
public void onItemClick(AdapterView parent, View v, int position, long id) {
Toast.makeText(getApplicationContext(), ((TextView) v).getText(), Toast.LENGTH_SHORT).show();
}
});
} 
}
 
```

 

**1.3 Demo**
------------

 

 

![](file:///D:/Mohsin/assets/assets/img/Gridview.png)
