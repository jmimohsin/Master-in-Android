 
**Gallery Example**
===================

One of the Android layout widget – Gallery has lessen the pain of developer when
one needs to use horizontally scrolling list specially in case of showing images
in gallery view. But sometimes we need to customize this gallery widget as per
requirement, for example navigating gallery using next-previous buttons which
are placed at left and right side of gallery, highlighting selected image with
border to make it more user friendly.  
Here is code for Gallery Implementation which includes following features :-

1. Horizontal gallery view  
2. Showing selected image from gallery in larger view  
3. Next-Previous buttons for gallery navigation  
4. Highlighting selected image in horizontal gallery view

 

**1.Code for GalleryDemoActivity.java** 
----------------------------------------

 

```java
package rk.tutorial.gallery.example;
import java.util.ArrayList;
import java.util.List;
import android.app.Activity;
import android.graphics.Bitmap;
import android.graphics.drawable.BitmapDrawable;
import android.graphics.drawable.Drawable;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.AdapterView;
import android.widget.AdapterView.OnItemSelectedListener;
import android.widget.Gallery;
import android.widget.ImageView;
import android.widget.ImageView.ScaleType;
public class GalleryDemoActivity extends Activity {
private ImageView selectedImageView;
private ImageView leftArrowImageView;
private ImageView rightArrowImageView;
private Gallery gallery;
private int selectedImagePosition = 0;
private List<Drawable> drawables;
private GalleryImageAdapter galImageAdapter;
@Override
public void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.main);
getDrawablesList();
setupUI();
}
private void setupUI() {
selectedImageView = (ImageView) findViewById(R.id.selected_imageview);
leftArrowImageView = (ImageView) findViewById(R.id.left_arrow_imageview);
rightArrowImageView = (ImageView) findViewById(R.id.right_arrow_imageview);
gallery = (Gallery) findViewById(R.id.gallery);
leftArrowImageView.setOnClickListener(new OnClickListener() {
@Override
public void onClick(View v) {
if (selectedImagePosition > 0) {
--selectedImagePosition;
}
gallery.setSelection(selectedImagePosition, false);
}
});
rightArrowImageView.setOnClickListener(new OnClickListener() {
@Override
public void onClick(View v) {
if (selectedImagePosition < drawables.size() - 1) {
++selectedImagePosition;
}
gallery.setSelection(selectedImagePosition, false);
}
});
gallery.setOnItemSelectedListener(new OnItemSelectedListener() {
@Override
public void onItemSelected(AdapterView parent, View view, int pos, long id) {
selectedImagePosition = pos;
if (selectedImagePosition > 0 && selectedImagePosition < drawables.size() - 1) {
leftArrowImageView.setImageDrawable(getResources().getDrawable(R.drawable.arrow_left_enabled));
rightArrowImageView.setImageDrawable(getResources().getDrawable(R.drawable.arrow_right_enabled));
} else if (selectedImagePosition == 0) {
leftArrowImageView.setImageDrawable(getResources().getDrawable(R.drawable.arrow_left_disabled));
} else if (selectedImagePosition == drawables.size() - 1) {
rightArrowImageView.setImageDrawable(getResources().getDrawable(R.drawable.arrow_right_disabled));
}
changeBorderForSelectedImage(selectedImagePosition);
setSelectedImage(selectedImagePosition);
}
@Override
public void onNothingSelected(AdapterView arg0) {
}
});
galImageAdapter = new GalleryImageAdapter(this, drawables);
gallery.setAdapter(galImageAdapter);
if (drawables.size() > 0) {
gallery.setSelection(selectedImagePosition, false);
}
if (drawables.size() == 1) {
rightArrowImageView.setImageDrawable(getResources().getDrawable(R.drawable.arrow_right_disabled));
}
}
private void changeBorderForSelectedImage(int selectedItemPos) {
int count = gallery.getChildCount();
for (int i = 0; i < count; i++) {
ImageView imageView = (ImageView) gallery.getChildAt(i);
imageView.setBackgroundDrawable(getResources().getDrawable(R.drawable.image_border));
imageView.setPadding(3, 3, 3, 3);
}
ImageView imageView = (ImageView) gallery.getSelectedView();
imageView.setBackgroundDrawable(getResources().getDrawable(R.drawable.selected_image_border));
imageView.setPadding(3, 3, 3, 3);
}

private void getDrawablesList() {
drawables = new ArrayList<Drawable>();
drawables.add(getResources().getDrawable(R.drawable.natureimage1));
drawables.add(getResources().getDrawable(R.drawable.natureimage2));
drawables.add(getResources().getDrawable(R.drawable.natureimage3));
drawables.add(getResources().getDrawable(R.drawable.natureimage4));
drawables.add(getResources().getDrawable(R.drawable.natureimage5));
drawables.add(getResources().getDrawable(R.drawable.natureimage6));
drawables.add(getResources().getDrawable(R.drawable.natureimage7));
drawables.add(getResources().getDrawable(R.drawable.natureimage8));
drawables.add(getResources().getDrawable(R.drawable.natureimage9));
drawables.add(getResources().getDrawable(R.drawable.natureimage10));
drawables.add(getResources().getDrawable(R.drawable.natureimage11));
drawables.add(getResources().getDrawable(R.drawable.natureimage12));
drawables.add(getResources().getDrawable(R.drawable.natureimage13));
drawables.add(getResources().getDrawable(R.drawable.natureimage14));
drawables.add(getResources().getDrawable(R.drawable.natureimage15));
}

private void setSelectedImage(int selectedImagePosition) {
BitmapDrawable bd = (BitmapDrawable) drawables.get(selectedImagePosition);
Bitmap b = Bitmap.createScaledBitmap(bd.getBitmap(), (int) (bd.getIntrinsicHeight() * 0.9), (int) (bd.getIntrinsicWidth() * 0.7), false);
selectedImageView.setImageBitmap(b);
selectedImageView.setScaleType(ScaleType.FIT_XY);
}
}
```

 

**2. Code for GalleryImageAdapter.java** 
-----------------------------------------

 

```java
package rk.tutorial.gallery.example;
import java.util.List;
import android.app.Activity;
import android.graphics.drawable.Drawable;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseAdapter;
import android.widget.Gallery;
import android.widget.ImageView;
public class GalleryImageAdapter extends BaseAdapter {
private Activity context;
private static ImageView imageView;
private List<Drawable> plotsImages;
private static ViewHolder holder;
public GalleryImageAdapter(Activity context, List<Drawable> plotsImages) {
this.context = context;
this.plotsImages = plotsImages;
}
@Override
public int getCount() {
return plotsImages.size();
}
@Override
public Object getItem(int position) {
return null;
}
@Override
public long getItemId(int position) {
return 0;
}
@Override
public View getView(int position, View convertView, ViewGroup parent) {
if (convertView == null) {
holder = new ViewHolder();
imageView = new ImageView(this.context);
imageView.setPadding(3, 3, 3, 3);
convertView = imageView;
holder.imageView = imageView;
convertView.setTag(holder);
} else {
holder = (ViewHolder) convertView.getTag();
}
holder.imageView.setImageDrawable(plotsImages.get(position));
holder.imageView.setScaleType(ImageView.ScaleType.CENTER_CROP);
holder.imageView.setLayoutParams(new Gallery.LayoutParams(80, 70));
return imageView;
}
private static class ViewHolder {
ImageView imageView;
}
}
 
```

 

**3. Code for main.xml** 
-------------------------

 

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:background="@android:color/white"
android:orientation="vertical" >
<ImageView
android:id="@+id/selected_imageview"
android:layout_width="fill_parent"
android:layout_height="fill_parent"
android:layout_above="@+id/gallery_relative_layout"
android:layout_marginLeft="10dip"
android:layout_margin="10dip"/>

<RelativeLayout
android:id="@+id/gallery_relative_layout"
android:layout_width="fill_parent"
android:layout_height="100dip"
android:layout_alignParentBottom="true"
android:orientation="horizontal" >

<ImageView
android:id="@+id/left_arrow_imageview"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:layout_centerVertical="true"
android:layout_marginLeft="10dip"
android:src="@drawable/arrow_left_disabled" />

<Gallery
android:id="@+id/gallery"
android:layout_width="80dip"
android:layout_height="700dip"
android:layout_marginLeft="5dip"
android:layout_marginRight="5dip"
android:layout_toLeftOf="@+id/right_arrow_imageview"
android:layout_toRightOf="@+id/left_arrow_imageview"
android:spacing="10dip" />

<ImageView
android:id="@+id/right_arrow_imageview"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:layout_alignParentRight="true"
android:layout_centerVertical="true"
android:layout_marginRight="10dip"
android:src="@drawable/arrow_right_enabled" />
</RelativeLayout>
</RelativeLayout>
```

 

**4. Demo:**
------------

 

![](file:///D:/Mohsin/assets/assets/img/gallery.png)
