**Android Database Example**
============================

 

Create the MySQLiteHelper class. This class is responsible for creating the
database. The onUpdate() method will simply delete all existing data and
re-create the table. It also defines several constants for the table name and
the table columns.

 

```java
import android.content.Context;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteOpenHelper;
import android.util.Log;
public class MySQLiteHelper extends SQLiteOpenHelper {
public static final String TABLE_COMMENTS = "comments";
public static final String COLUMN_ID = "_id";
public static final String COLUMN_COMMENT = "comment";
private static final String DATABASE_NAME = "commments.db";
private static final int DATABASE_VERSION = 1;
// Database creation sql statement
private static final String DATABASE_CREATE = "create table " + TABLE_COMMENTS + "(" + COLUMN_ID + " integer primary key autoincrement, " + COLUMN_COMMENT + " text not null);";
public MySQLiteHelper(Context context) {

super(context, DATABASE_NAME, null, DATABASE_VERSION);
}
@Override
public void onCreate(SQLiteDatabase database) {

database.execSQL(DATABASE_CREATE);
}
@Override
public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {

Log.w(MySQLiteHelper.class.getName(), "Upgrading database from version " + oldVersion + " to " + newVersion + ", which will destroy all old data");
db.execSQL("DROP TABLE IF EXISTS " + TABLE_COMMENTS);
onCreate(db);
}
}
```

Create the Comment class. This class is our model and contains the data we will
save in the database and show in


```java
public class Comment {
private long id;
private String comment;
public long getId() {
return id;
}
public void setId(long id) {
this.id = id;
}
public String getComment() {

return comment;
}
public void setComment(String comment) {
this.comment = comment;
}
// Will be used by the ArrayAdapter in the ListView
@Override
public String toString() {
return comment;
}
}
 
```

Create the CommentsDataSource class. This class is our DAO. It maintains the
database connection and supports adding new comments and fetching all comments.


```java
import java.util.ArrayList;
import java.util.List;
import android.content.ContentValues;
import android.content.Context;
import android.database.Cursor;
import android.database.SQLException;
import android.database.sqlite.SQLiteDatabase;
public class CommentsDataSource {
// Database fields
private SQLiteDatabase database;
private MySQLiteHelper dbHelper;
private String[] allColumns = { MySQLiteHelper.COLUMN_ID, MySQLiteHelper.COLUMN_COMMENT };
public CommentsDataSource(Context context) {
dbHelper = new MySQLiteHelper(context);
}
public void open() throws SQLException {
database = dbHelper.getWritableDatabase();
}
public void close() {
dbHelper.close();
}
public Comment createComment(String comment) {

ContentValues values = new ContentValues();
values.put(MySQLiteHelper.COLUMN_COMMENT, comment);
long insertId = database.insert(MySQLiteHelper.TABLE_COMMENTS, null, values);
Cursor cursor = database.query(MySQLiteHelper.TABLE_COMMENTS, allColumns, MySQLiteHelper.COLUMN_ID + " = " + insertId, null, null, null, null);
cursor.moveToFirst();
Comment newComment = cursorToComment(cursor);
cursor.close();
return newComment;
}
public void deleteComment(Comment comment) {
long id = comment.getId();
System.out.println("Comment deleted with id: " + id);
database.delete(MySQLiteHelper.TABLE_COMMENTS, MySQLiteHelper.COLUMN_ID + " = " + id, null);
}
public List<Comment> getAllComments() {
List<Comment> comments = new ArrayList<Comment>();
Cursor cursor = database.query(MySQLiteHelper.TABLE_COMMENTS, allColumns, null, null, null, null, null);
cursor.moveToFirst();
while (!cursor.isAfterLast()) {
Comment comment = cursorToComment(cursor);
comments.add(comment);
cursor.moveToNext();
}
// Make sure to close the cursor
cursor.close();
return comments;
}
private Comment cursorToComment(Cursor cursor) {
Comment comment = new Comment();
comment.setId(cursor.getLong(0));
comment.setComment(cursor.getString(1));
return comment;
}
}
```


 

**User Interface**
------------------

  
Change your main.xml layout file in the res/layout folder to the following. This
layout has two buttons for adding and deleting comments and a ListView which
will be used to display the existing comments. The comment text will be
generated later in the Activity by a small random generator.


```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:orientation="vertical" >

<LinearLayout
android:id="@+id/group"
android:layout_width="wrap_content"
android:layout_height="wrap_content" >

<Button
android:id="@+id/add"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Add New" 
android:onClick="onClick"/>

<Button
android:id="@+id/delete"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Delete First" 
android:onClick="onClick"/>
</LinearLayout>
<ListView
android:id="@android:id/list"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:text="@string/hello" />
</LinearLayout>
```


Change your TestDatabaseActivity class. to the following. We use here a
ListActivity for displaying the data.


```java
import java.util.List;
import java.util.Random;
import android.app.ListActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.ArrayAdapter;
public class TestDatabaseActivity extends ListActivity {
private CommentsDataSource datasource;

@Override
public void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.main);
datasource = new CommentsDataSource(this);
datasource.open();
List<Comment> values = datasource.getAllComments();
// Use the SimpleCursorAdapter to show the
// elements in a ListView
ArrayAdapter<Comment> adapter = new ArrayAdapter<Comment>(this, android.R.layout.simple_list_item_1, values);
setListAdapter(adapter);
}

// Will be called via the onClick attribute
// of the buttons in main.xml
public void onClick(View view) {
@SuppressWarnings("unchecked")
ArrayAdapter<Comment> adapter = (ArrayAdapter<Comment>) getListAdapter();
Comment comment = null;
switch (view.getId()) {
case R.id.add:
String[] comments = new String[] { "Cool", "Very nice", "Hate it" };
int nextInt = new Random().nextInt(3);
// Save the new comment to the database
comment = datasource.createComment(comments[nextInt]);
adapter.add(comment);
break;
case R.id.delete:
if (getListAdapter().getCount() > 0) {
comment = (Comment) getListAdapter().getItem(0);
datasource.deleteComment(comment);
adapter.remove(comment);
}
break;
}
adapter.notifyDataSetChanged();
}
@Override
protected void onResume() {
datasource.open();
super.onResume();
}
@Override
protected void onPause() {
datasource.close();
super.onPause();
}
}
```


![](img/Database.png)
