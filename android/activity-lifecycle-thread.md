
# Activity life Cycle

The following example will download an image from the Internet in a thread and displays a dialog until the download is done. We will make sure that the thread is preserved even if the activity is restarted and that the dialog is correctly displayed and closed.  
For this example create the Android project "de.vogella.android.threadslifecycle" and the Activity "ThreadsLifecycleActivity". Also add the permission to use the Internet to your app.

  
### 1. AndroidManifest
  

You should have the following AndroidManifest.xml file.

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
	package="de.vogella.android.threadslifecycle"
	android:versionCode="1"
	android:versionName="1.0" >
<uses-sdk android:minSdkVersion="10" />
	<uses-permission android:name="android.permission.INTERNET" >
</uses-permission>
<application
	android:icon="@drawable/icon"
	android:label="@string/app_name" >
	<activity
	android:name=".ThreadsLifecycleActivity"
	android:label="@string/app_name" >
	<intent-filter>
		<action android:name="android.intent.action.MAIN" />
		<category android:name="android.intent.category.LAUNCHER" />
	</intent-filter>
	</activity>
</application> 
</manifest>
```

### 2. main layout

  
Change the layout main.xml to the following.
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
	android:layout_width="match_parent"
	android:layout_height="match_parent"
	android:orientation="vertical" >

	<LinearLayout
		android:id="@+id/linearLayout1"
		android:layout_width="match_parent"
		android:layout_height="wrap_content" >

		<Button
			android:layout_width="wrap_content"
			android:layout_height="wrap_content"
			android:onClick="downloadPicture"
			android:text="Click to start download" >
		</Button>

		<Button
			android:layout_width="wrap_content"
			android:layout_height="wrap_content"
			android:onClick="resetPicture"
			android:text="Reset Picture" >
		</Button>
	</LinearLayout>
	<ImageView
		android:id="@+id/imageView1"
		android:layout_width="match_parent"
		android:layout_height="match_parent"
		android:src="@drawable/icon" >
	</ImageView>
</LinearLayout>
```

### 3. Activity
  

Now adjust your activity. In this activity the thread is saved and the dialog is closed if the activity is destroyed.
```java
import java.io.IOException;
import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.StatusLine;
import org.apache.http.client.HttpClient;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.client.methods.HttpUriRequest;
import org.apache.http.impl.client.DefaultHttpClient;
import org.apache.http.util.EntityUtils;
import android.app.Activity;
import android.app.ProgressDialog;
import android.graphics.Bitmap;
import android.graphics.BitmapFactory;
import android.os.Bundle;
import android.os.Handler;
import android.view.View;
import android.widget.ImageView;
public class ThreadsLifecycleActivity extends Activity {
	// Static so that the thread access the latest attribute
	private static ProgressDialog dialog;
	private static ImageView imageView;
	private static Bitmap downloadBitmap;
	private static Handler handler;
	private Thread downloadThread;
	/* Called when the activity is first created. */

	@Override
	public void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main);
		//Create a handler to update the UI
		handler = new Handler();
		//get the latest imageView after restart of the application
		imageView = (ImageView) findViewById(R.id.imageView1);
		//Did we already download the image?
		if (downloadBitmap != null) {
			imageView.setImageBitmap(downloadBitmap);
		}
		//Check if the thread is already running
		downloadThread = (Thread) getLastNonConfigurationInstance();
		if (downloadThread != null && downloadThread.isAlive()) {
			dialog = ProgressDialog.show(this, "Download", "downloading");
		}
	}

	public void resetPicture(View view) {
		if (downloadBitmap != null) {
			downloadBitmap = null;
		}
		imageView.setImageResource(R.drawable.icon);
	}

	public void downloadPicture(View view) {
		dialog = ProgressDialog.show(this, "Download", "downloading");
		downloadThread = new MyThread();
		downloadThread.start();
	}

	// Save the thread
	@Override
	public Object onRetainNonConfigurationInstance() {
	return downloadThread;
	}

	// dismiss dialog if activity is destroyed
	@Override
	protected void onDestroy() {

	if (dialog != null && dialog.isShowing()) {
	dialog.dismiss();
	dialog = null;
	}
	super.onDestroy();
	}

	// Utiliy method to download image from the internet
	static private Bitmap downloadBitmap(String url) throws IOException {
	HttpUriRequest request = new HttpGet(url.toString());
	HttpClient httpClient = new DefaultHttpClient();
	HttpResponse response = httpClient.execute(request);
	StatusLine statusLine = response.getStatusLine();
	int statusCode = statusLine.getStatusCode();
	if (statusCode == 200) {
		HttpEntity entity = response.getEntity();
		byte[] bytes = EntityUtils.toByteArray(entity);
		Bitmap bitmap = BitmapFactory.decodeByteArray(bytes, 0, bytes.length);
		return bitmap;
	} else {
		throw new IOException("Download failed, HTTP response code " + statusCode + " \- " + statusLine.getReasonPhrase());
	}

	}

	static public class MyThread extends Thread {
		@Override
		public void run() {
		   try {
		// Simulate a slow network
			try {
			new Thread().sleep(5000);
			}catch (InterruptedException e) {
				e.printStackTrace();
		}
		downloadBitmap = downloadBitmap("http://www.vogella.com/img/lars/LarsVogelArticle7.png");
		handler.post(new MyRunnable());
		} catch (IOException e) {
		e.printStackTrace();
		}
	 }
	}

	static public class MyRunnable implements Runnable {
		public void run() 
		{
			imageView.setImageBitmap(downloadBitmap);
			dialog.dismiss();
		}
	}
}
```
Run your application and press the button to start a download. You can test the correct lifecycle behavior in the emulator via pressing "Ctrl+F11" as this changes the orientation.  
It is important to note that the Thread is a static inner class. It is important to use a static inner class for your background process because otherwise the inner class will contain a reference to the class in which is was created. As the thread is passed to the new instance of your activity this would create a memory leak as the old activity would still be referred to by the Thread.
