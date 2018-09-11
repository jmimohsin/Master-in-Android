**Progressbar Example**
=======================

In this tutorial, we show you how to display a progress bar dialog to tell user
that your task is running, and also how to increase the progress bar status
until the task is completed.  
  


**1. Add a Button**<br><br>
---------------------------

Open “res/layout/main.xml” file, just add normal button for demonstration.  
File : res/layout/activity_main.xml

```xml
<?xml version="1.0" encoding="utf-8"?> 
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android" 
android:layout_width="fill_parent" 
android:layout_height="fill_parent" 
android:orientation="vertical" 
android:gravity="center_horizontal">

<Button
android:layout_margin="20dip"
android:id="@+id/btnStartProgress"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Download File" />
</LinearLayout>
```

 

**2. Activity** <br><br>
------------------------

The key to use progress bar is using “Thread” to run your time consume task and
another “Thread” to update the progress bar status accordingly. Read the code’s
comment, it should be self-explanatory.  
File : MainActivity.java

```java
package rk.tutorial.progress.bar.example;
import android.os.Bundle;
import android.os.Handler;
import android.app.Activity;
import android.app.ProgressDialog;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.support.v4.app.NavUtils;
public class MainActivity extends Activity {
Button btnStartProgress;
ProgressDialog progressBar;
private int progressBarStatus = 0;
private Handler progressBarHandler = new Handler();
private long fileSize = 0;
@Override
public void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.activity_main);
addListenerOnButton();
}

public void addListenerOnButton() {
btnStartProgress = (Button) findViewById(R.id.btnStartProgress);
btnStartProgress.setOnClickListener( new OnClickListener() {
@Override public void onClick(View v) {
// prepare for a progress bar dialog
progressBar = new ProgressDialog(v.getContext());
progressBar.setCancelable(true);
progressBar.setMessage("File downloading ...");
progressBar.setProgressStyle(ProgressDialog.STYLE_HORIZONTAL);
progressBar.setProgress(0);
progressBar.setMax(100);
progressBar.show();
//reset progress bar status
progressBarStatus = 0;
//reset filesize
fileSize = 0;
new Thread(new Runnable() {
public void run() {
while (progressBarStatus < 100) {
// process some tasks
progressBarStatus = doSomeTasks();
// your computer is too fast, sleep 1 second
try {
Thread.sleep(1000);
} catch (InterruptedException e) {
e.printStackTrace();
}
// Update the progress bar
progressBarHandler.post(new Runnable() {
public void run() {
progressBar.setProgress(progressBarStatus);
}
});
}
// ok, file is downloaded,
if (progressBarStatus >= 100) {
// sleep 2 seconds, so that you can see the 100%
try {
Thread.sleep(2000);
} catch (InterruptedException e) {
e.printStackTrace();
}
// close the progress bar dialog
progressBar.dismiss();
}
}
}).start();
}
});
}
// file download simulator... a really simple
public int doSomeTasks() {

while (fileSize <= 1000000) {
fileSize++;
if (fileSize == 100000) {
return 10;
} else if (fileSize == 200000) {
return 20;
} else if (fileSize == 300000) {
return 30;
}
// ...add your own
}
return 100;
}
}
```

 

**3. Demo** 
------------

  
Run the application.  
1. Result, a single button.  


![](file:///D:/Mohsin/assets/assets/img/progress.png)

![](file:///D:/Mohsin/assets/assets/img/progress-bar.png)
