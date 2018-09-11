# Content Provider


Irrespective of how the data is stored, Content Providers give a uniform
interface to access the data. Data is exposed as a simple table with rows and
columns where row is a record and column is a particular data type with a
specific meaning. Like a row could be about a single person and the columns
could be the person’s first name, number, address, email id etc.  
Each record is identified by a unique \_ID field which is the key to the record.
Each content provider exposes a unique URI that identifies its data set
uniquely. This URI is equivalent to a table name in a database. The URI consists
of various parts: eg: content://com.colllabera.labs.sai/tasks/123 is a unique
URI. content:// is a standard prefix. com.collabera.labs.sai is the authority,
tasks is the table name, 123 is the unique \_ID.  
For the native content providers, these unique URIs are declared as constants in
an interface. So, in our program we will be using constants like
People.CONTENT_URI which internally translates to content://contacts/people  
Let us now look at the code to view all the existing contacts:

  
//Here is the button to click for viewing the contacts

```java
Button view = (Button)findViewById(R.id.viewButton);
```

…  
//The method / class that gets invoked when the View button is clicked

```java
view.setOnClickListener(new OnClickListener() {
public void onClick(View v){
displayContacts();
Log.i("NativeContentProvider", "Completed Displaying Contact list");
}
});
…
```

//Here is the displayContacts() method

```java
private void displayContacts() {
String[] columns = new String[] {People.NAME,People.NUMBER};
Uri mContacts = People.CONTENT_URI;
Cursor mCur = managedQuery(mContacts, // Contact URI
columns, // Which columns to return
null, // Which rows to return
null, // Where clause parameters
null // Order by clause
);
if (mCur.moveToFirst()) {
String name = null;
String phoneNo = null;
do {
name = mCur.getString(mCur.getColumnIndex(People.NAME));
phoneNo = mCur.getString(mCur.getColumnIndex(People.NUMBER));
Toast.makeText(NativeContentProvider.this, name + " " + phoneNo, Toast.LENGTH_SHORT).show();
} while (mCur.moveToNext());
}
}
````

Here we are using the Activity.managedQuery(..) to create and execute a query
against the provided URI. The comments against the parameters in the code is
self-explanatory. This returns a cursor object that can be iterated using the
two methods moveToFirst() and moveToNext(). For simplicity sake, I have just
toasted the contact name and phone number retrieved. An advanced tutorial can
start a new activity that can display this in a ListView.  
Now, we can move on to creating a new contact. While the button related code
will be very similar to the above, let us look at the actual createContact()
method.

```java
private void createContact(String name, String phone) {
ContentValues contact = new ContentValues();
contact.put(People.NAME, name);
insertUri = getContentResolver().insert(People.CONTENT_URI, contact);
Log.d(getClass().getSimpleName(),insertUri.toString());
Uri phoneUri = Uri.withAppendedPath(insertUri, People.Phones.CONTENT_DIRECTORY);
contact.clear();
contact.put(People.Phones.TYPE, People.TYPE_MOBILE);
contact.put(People.NUMBER, phone);
updateUri = getContentResolver().insert(phoneUri, contact);
Toast.makeText(NativeContentProvider.this, "Created a new contact: " + name + " " + phone, Toast.LENGTH_SHORT).show();
Log.d(getClass().getSimpleName(),updateUri.toString());
}
```

Here we need to understand 2 new classes: ContentResolver and ContentValues. A
ContentResolver provides applications access to the content data / model. We can
get a handle to a ContentResolver by calling the getContentResolver() method
within the Activity. This provides methods to insert, update and delete data. In
order to insert data, we need to provide it through a ContentValues object. A
ContentValues Object is nothing but a name, value pair where the name of the
column is to be mentioned. So, we pass the URI and the ContentValues to insert()
method which returns a unique URI with the new ID created. Once we get the ID of
the new person/contact inserted, we insert his/her mobile phone details into the
related Phones table by using the returned insertUri. The insertUri which is
unique to the new record is stored as a class variable to use it in the delete
method later. The phoneUri is also stored for updating the same in the
updateContact() method later.  
Note that People is a class that has implemented various interfaces like
android.priovider.BaseColumns, android.provider.Contacts.Phones,
android.provider.Contact.PeopleColumns etc. These constants come from the
interfaces.  
With the above understanding let us see the update and delete methods:

```java
private void updateContact(String phone) {
if (updateUri == null) {
Toast.makeText(NativeContentProvider.this, "There is nothing to update, Please create a contact and then click update", Toast.LENGTH_LONG).show();
} else {
ContentValues newPhone = new ContentValues();
newPhone.put(People.Phones.TYPE, People.TYPE_MOBILE);
newPhone.put(People.NUMBER, phone);
getContentResolver().update(updateUri, newPhone, null,null);
Toast.makeText(NativeContentProvider.this, "Updated the phone number to: " + phone, Toast.LENGTH_SHORT).show();
Log.i(getClass().getSimpleName(), "Updated the phone number");
}
}
private void deleteContact() {
if (updateUri == null) {
Toast.makeText(NativeContentProvider.this, "Please create a contact by clicking create button, then I can delete the same", Toast.LENGTH_LONG).show();
} else {
getContentResolver().delete(insertUri, null, null);
Toast.makeText(NativeContentProvider.this, "Deleted contact at: " + insertUri.toString(), Toast.LENGTH_SHORT).show();
updateUri = null;
insertUri = null;
Log.i(getClass().getSimpleName(),"Deleted the contact inserted by this program");
}
}
```

These methods only manipulate the freshly created record, for simplicity sake.
They call upon the update() and delete() method on the ContentResolver.  
The complete code for this example is available here.  
Please note that you must add the following permissions to the
AndroidManifest.xml file to be able to access the contacts.

```java
<uses-permission android:name="android.permission.READ_CONTACTS"></uses-permission>
<uses-permission android:name="android.permission.WRITE_CONTACTS"></uses-permission>
 
```

Otherwise you get a SecurityException.
