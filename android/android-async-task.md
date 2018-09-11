**Async Task**
==============

The AsyncTask class encapsulates the creation of Threads and Handlers. An
AsyncTask is started via the execute() method.  
The execute() method calls the doInBackground() and the onPostExecute() method.  
The doInBackground() method contains the coding instruction which should be
performed in a background thread. This method runs automatically in a separate
Thread.  
The onPostExecute() method synchronize itself again with the user interface
thread and allows to update it. This method is called by the framework once the
doInBackground() method finishes.  
To use AsyncTask you must subclass it. AsyncTask uses generics and varargs. The
parameters are the following AsyncTask .  
TypeOfVarArgParams is passed into the doInBackground() method as input,
ProgressValue is used for progress information and ResultValue must be returned
from doInBackground() method and is passed to onPostExecute() as parameter.  
In this example we will use an instance of the AsyncTask class to download the
content of a webpage. We use Android HttpClient for this. Create a new Android
project called de.vogella.android.asynctask with an Activity called
ReadWebpageAsyncTask. Add the android.permission.INTERNET permission to your
\<filenname\>AndroidManifest.xml file. .

<br><br>**1. Layout**
---------------------

  
Create the following layout.

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:orientation="vertical" >

<Button
android:id="@+id/readWebpage"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:onClick="readWebpage"
android:text="Load Webpage" >
</Button>

<TextView
android:id="@+id/TextView01"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:text="Example Text" >
</TextView>
</LinearLayout>
```

 

**2. Activity**
---------------

  
Change your activity to the following:

```java
import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import org.apache.http.HttpResponse;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.impl.client.DefaultHttpClient;
import android.app.Activity;
import android.os.AsyncTask;
import android.os.Bundle;
import android.view.View;
import android.widget.TextView;
public class ReadWebpageAsyncTask extends Activity {
private TextView textView;
/** Called when the activity is first created. */
@Override
public void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.main);
textView = (TextView) findViewById(R.id.TextView01);
}
private class DownloadWebPageTask extends AsyncTask {
@Override
protected String doInBackground(String... urls) {

String response = "";
for (String url : urls) {
DefaultHttpClient client = new DefaultHttpClient();
HttpGet httpGet = new HttpGet(url);
try {
HttpResponse execute = client.execute(httpGet);
InputStream content = execute.getEntity().getContent();
BufferedReader buffer = new BufferedReader(new InputStreamReader(content));
String s = "";
while ((s = buffer.readLine()) != null) {
response += s;
}
} catch (Exception e) {
e.printStackTrace();
}
}
return response;
}
@Override
protected void onPostExecute(String result) {
textView.setText(result);
}
}
public void readWebpage(View view) {

DownloadWebPageTask task = new DownloadWebPageTask();
task.execute(new String[] { "http://www.vogella.com" });
}
} 
```

If you run your application and press your button then the content of the
defined webpage should be read in the background. Once this process is done your
TextView will be updated.  

