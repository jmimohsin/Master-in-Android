
## Defining an AIDL Interface

The AIDL syntax is very similar to regular Java interface. You simply define the method signature. The datatypes supported by AIDL are somewhat different than regular Java interfaces. For one, all Java primitive datatypes are supported. So are String, List, Map, and CharSequence classes. Also, all other AIDL datatypes that you defined are supported. In addition to that, all Parcelable classes are supported, but this is not going to be covered in this example. I'm trying to keep this example somewhat simpler to start with.

You must define your AIDL interface in an aidl file using the Java programming language syntax, then save it in the source code (in the src/ directory) of both the application hosting the service and any other application that binds to the service.

When you build each application that contains the aidl file, the Android SDK tools generate an interface based on the aidl file and save it in the project's gen/ directory. The service must implement the interface as appropriate. The client applications can then bind to the service and call methods from the IBinder to perform IPC.

To create a bounded service using AIDL, follow these steps:

**1.  Create the .aidl file**

This file defines the programming interface with method signatures.

**2.  Implement the interface**

The Android SDK tools generate an interface in the Java programming language, based on your aidl file. This interface has an inner abstract class named Stub that extends Binder and implements methods from your AIDL interface. You must extend the Stub class and implement the methods.

**3.  Expose the interface to clients**

Implement a Service and override onBind() to return your implementation of the Stub class.

**/src/com.marakana/IAdditionService.aidl**

Code:  
  
```java
package com.marakana;

// Declare the interface.
interface IAdditionService {
    // You can pass values in, out, or inout. 
    // Primitive datatypes (such as int, boolean, etc.) can only be passed in.
    int add(in int value1, in int value2);
}
```
  
### Implementing the Remote Service
  
Once you create your AIDL file and put it in the right place, the Eclipse+AIDL tool will generate a file with the same name, but .java extension. So I now have /gen/com.marakana.com/IAdditionService.java file. This is an auto-generated file so you don't want to edit it. What is important is that it contains a Stub class that we'll want to implement for our remote service.  
  
To implement our remote service, we'll return the IBinder from onBind() method in our service class, AdditionService. The IBinder represents the implementation of the remote service. To implement IBinder, we subclass IAddtionService.Stub class from the auto-generated Java code, and provide implementation for our AIDL-defined methods, in this case add().  
  
**/src/com.marakana/AdditionService.java**

Code:  
  
```java
package com.marakana;

import android.app.Service;
import android.content.Intent;
import android.os.IBinder;
import android.os.RemoteException;
import android.util.Log;

/*This class exposes the remote service to the client*/
public class AdditionService extends Service {
  private static final String TAG = "AdditionService";
  
  @Override
  public void onCreate() {
    super.onCreate();
    Log.d(TAG, "onCreate()");
  }
  
  @Override
  public IBinder onBind(Intent intent) {

    return new IAdditionService.Stub() {
    /*Implementation of the add() method */
      public int add(int value1, int value2) throws RemoteException {
        Log.d(TAG, String.format("AdditionService.add(%d, %d)",value1, value2));
        return value1 + value2;
      }

    };
  }

  @Override
  public void onDestroy() {
    super.onDestroy();
    Log.d(TAG, "onDestroy()");
  }
}
```
  
### Exposing the Service Locally
  
Once we have the service implement the onBind() properly, we are ready to connect to that service from our client. In this case, we have AIDLDemo activity connecting to that service. To establish the connection, we need to implement ServiceConnection class. Our activity in this example provides this implementation in AdditionServiceConnection inner class by implementing onServiceConnected() and onServiceDiconnected() methods. Those callbacks will get the stub implementation of the remote service upon connection. We need to cast them from stubs to our AIDL service implementation. To do that, we use the IAdditionService.Stub.asInterface(IBinder) boundService) helper method.  
  
From that point on, we have a local service object that we can use to make calls against the remote service.  
  
**/src/com.marakana/AIDLDemo.java**

Code:  
  
```java
package com.marakana;

import android.app.Activity;
import android.content.ComponentName;
import android.content.Context;
import android.content.Intent;
import android.content.ServiceConnection;
import android.os.Bundle;
import android.os.IBinder;
import android.os.RemoteException;
import android.util.Log;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

public class AIDLDemo extends Activity {
  private static final String TAG = "AIDLDemo";
  IAdditionService service;
  AdditionServiceConnection connection;

  
 /*This class represents the actual service connection. It casts the bound*/
 /*stub implementation of the service to the AIDL interface.*/
 
  class AdditionServiceConnection implements ServiceConnection {

    public void onServiceConnected(ComponentName name, IBinder boundService) {
      service = IAdditionService.Stub.asInterface((IBinder) boundService);
      Log.d(AIDLDemo.TAG, "onServiceConnected() connected");
      Toast.makeText(AIDLDemo.this, "Service connected", Toast.LENGTH_LONG)
          .show();
    }

    public void onServiceDisconnected(ComponentName name) {
      service = null;
      Log.d(AIDLDemo.TAG, "onServiceDisconnected() disconnected");
      Toast.makeText(AIDLDemo.this, "Service connected", Toast.LENGTH_LONG)
          .show();
    }
  }

  /* Binds this activity to the service. */
  private void initService() {
    connection = new AdditionServiceConnection();
    Intent i = new Intent();
    i.setClassName("com.marakana", com.marakana.AdditionService.class.getName());
    boolean ret = bindService(i, connection, Context.BIND\_AUTO\_CREATE);
    Log.d(TAG, "initService() bound with " + ret);
  }

  /* Unbinds this activity from the service. */
  private void releaseService() {
    unbindService(connection);
    connection = null;
    Log.d(TAG, "releaseService() unbound.");
  }

  /* Called when the activity is first created. */
  @Override
  public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.main);

    initService();

    // Setup the UI
    Button buttonCalc = (Button) findViewById(R.id.buttonCalc);

    buttonCalc.setOnClickListener(new OnClickListener() {
      TextView result = (TextView) findViewById(R.id.result);
      EditText value1 = (EditText) findViewById(R.id.value1);
      EditText value2 = (EditText) findViewById(R.id.value2);

      public void onClick(View v) {
        int v1, v2, res = -1;
        v1 = Integer.parseInt(value1.getText().toString());
        v2 = Integer.parseInt(value2.getText().toString());

        try {
          res = service.add(v1, v2);
        } catch (RemoteException e) {
          Log.d(AIDLDemo.TAG, "onClick failed with: " + e);
          e.printStackTrace();
        }
        result.setText(new Integer(res).toString());
      }
    });
  }

  /* Called when the activity is about to be destroyed. */
  @Override
  protected void onDestroy() {
    releaseService();
  }

}
```
  
The UI in this case is very simple. There are couple of TextViews and EditText fields and a button The button handles its events in an anonymous inner class OnClickListener. The button simply invokes the add() method on the service as if it was a local call.  
  
  
The layout for this example is not that significant, but I'm including it here for completeness purposes.  
  
**/res/layout/main.xml**

Code:  
  
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
  android:orientation="vertical" 
  android:layout_width="fill_parent"
  android:layout_height="fill_parent">
  <TextView android:layout_width="fill_parent"
    android:layout_height="wrap_content" 
    android:text="AIDL Demo"
    android:textSize="22sp" />
  <EditText android:layout_width="wrap_content"
    android:layout_height="wrap_content" 
    android:id="@+id/value1"
    android:hint="Value 1">
 </EditText>
  <TextView android:id="@+id/TextView01" 
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" 
    android:text="+"
    android:textSize="36sp">
   </TextView>
  <EditText  
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" 
    android:id="@+id/value2"
    android:hint="Value 2">
  </EditText>
  <Button   
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"             
    android:id="@+id/buttonCalc"
    android:text="=">
  </Button>
  <TextView   
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" 
    android:text="result"
    android:textSize="36sp" 
    android:id="@+id/result">
 </TextView>
</LinearLayout>
```
  
  
The output of your code should look like this:  
  
**Output**  

![](img/AIDL.png)
