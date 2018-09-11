**Basic Parsable Example**
==========================

There are built in functions in Intent to send ArrayList of primitive objects
e.g. String, Integer, but when it comes to Custom Data Handling Objects, BOOM…
you need to take that extra pain…..  
Android has defined a new light weight IPC (Inter Process Communication) data
structure called Parcel, where you can flatten your objects in byte stream, same
as J2SDK’s Serialization concept.  
So let’s come back to my original requirement, I had a Data Handling class,
which groups together a set of information-

<br>**In the first Activity:** <br><br>
---------------------------------------

// in CollectDataActivity, populate the Parcelable User object using its setter
methods

```java
User usr = new User();
usr.setId(id); // collected from user input// etc..
```

// pass it to another component

```java
Intent in = new Intent(this, ProcessDataActivity.class);
in.putExtra("user", usr);
startActivity(in);
```

end of first Activity :::::  
  


**In the second Activity:** <br><br>
------------------------------------

// in ProcessDataActivity retrieve User

```java
Intent intent = getIntent();
User usr = (User) intent.getParcelableExtra("user");
```

 

end of second Activity:::::  
  


**And this is what a Parcelable User class looks like:**

```java
import android.os.Parcel;
import android.os.Parcelable;
public class User implements Parcelable {
private long id;
private int age;
private String phone;
private boolean registered;
// No-arg Ctor
public User(){}
// all getters and setters go here //...
/** Used to give additional hints on how to process the received parcel.*/
@Override
public int describeContents() {
// ignore for now
return 0;
}

@Override
public void writeToParcel(Parcel pc, int flags) {
pc.writeLong(id);
pc.writeInt(age);
pc.writeString(phone);
pc.writeInt( registered ? 1 :0 );
}

/* Static field used to regenerate object, individually or as arrays */
public static final Parcelable.Creator<User> CREATOR = new Parcelable.Creator<User>() {
public User createFromParcel(Parcel pc) {
return new User(pc);
}

public User[] newArray(int size) {
return new User[size];
}
};

/*Ctor from Parcel, reads back fields IN THE ORDER they were written */
public User(Parcel pc){
id = pc.readLong();
age = pc.readInt();
phone = pc.readString();
registered = ( pc.readInt() == 1 );
}
}
```

 

**What we did was:**
--------------------

  
1. Make our User class implement the Parcelable interface. Parcelable is not a
marker interface, hence what follows:  
2. Implement its describeContents method, which in this case does nothing.  
3. Implement its abstract method writeToParcel, which takes the current state of
the object and writes it to a Parcel  
4. Add a static field called CREATOR to our class, which is an object
implementing the Parcelable.Creator interface  
5. Add a Constructor that takes a Parcel as parameter. The CREATOR calls that
constructor to rebuild our object.  
This looks like a lot of extra code at first, but bear in mind that, as in most
cases, our application might evolve into incorporating more data from the
user... Sometimes we need to pass complex objects from one component to another,
and passing an object yields a cleaner design.
