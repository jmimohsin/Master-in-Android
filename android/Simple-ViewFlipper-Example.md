**Simple View Flipper Example**
===============================

The ViewFlipper is a really useful view on android. It allows you to build up a
set of pages and easily move between them. At its simplest, you call the
showPrevious and showNext methods on the view and it moves through your pages
and wraps back to the beginning when it gets to the end. At the other end of the
spectrum you can incorporate gestures to enable the user to swipe through the
pages, and with the ViewFlipper handling just three views you can allow the user
to move through any number of pages.  
So, this application is going to show two buttons at the top to allow the user
to go to the next and previous pages. Beneath them will be the ViewFlipper which
contains three TextViews.  
So firstly create a new android project called ViewFlipperSimple and change the
res/layout/main.xml file to be the following:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="fill_parent" 
android:layout_height="fill_parent"
android:orientation="vertical">

<LinearLayout
android:layout_width="wrap_content" 
android:layout_height="wrap_content">

<Button 
android:id="@+id/previous" 
android:layout_width="wrap_content"
android:layout_height="wrap_content" 
android:text="Prev" />

<Button 
android:id="@+id/next" 
android:layout_width="wrap_content"
android:layout_height="wrap_content" 
android:text="Next" />
</LinearLayout>

<ViewFlipper
android:id="@+id/flipper" 
android:layout_width="fill_parent" 
android:layout_height="fill_parent">

<TextView
android:text="view 1"
android:layout_width="fill_parent" 
android:layout_height="fill_parent" />

<TextView
android:text="view 2"
android:layout_width="fill_parent" 
android:layout_height="fill_parent" />

<TextView
android:text="view 3"
android:layout_width="fill_parent" 
android:layout_height="fill_parent" />
</ViewFlipper>
</LinearLayout>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Now replace the contents of ViewFlipperSimple.java with:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
import android.app.Activity;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.ViewFlipper;
public class ViewFlipperSimple extends Activity implements OnClickListener {
Button next;
Button previous;
ViewFlipper flipper;
@Override
public void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.main);
flipper = (ViewFlipper)findViewById(R.id.flipper);
next = (Button) findViewById(R.id.next);
previous = (Button) findViewById(R.id.previous);
next.setOnClickListener(this);
previous.setOnClickListener(this);
}
@Override
public void onClick(View v) {
if (v == next) {
flipper.showNext();
}
else if (v == previous) {
flipper.showPrevious();
}
}
}
 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
