**XML Drawables**
=================

Android provides a number of drawable resources, many of which are defined
solely in XML. These drawables offer a wide range of flexibility and are a very
powerful tool that are often under-utilized. In this post and the next I will
focus only on Shape Drawable resources.

Shape drawables provide four basic shapes: Rectangle, Oval, Line, and Ring. From
these shapes you can create an almost unlimited number of effects and styles for
your application.

It should be noted that these effects are pretty basic... If you want to have
shiny gloss effects or anything like that you will need to use image editing
software to create the desired effect. However, these resources can be used to
create very appealing user interfaces for your Android apps.

All four shape types support the following tags (some of the shapes support
additional tags, but this is the set supported by all of them):

**gradient:** gradient backgrounds  
**solid:** Specify solid background color  
**padding:** padding between the edge of the shape and its contents  
**size:** Specify the width and height  
**stroke:** Specify a stroke line around the edge of the shape

**Rectangle**<br>
-----------------

One of the most basic shapes, and one of the most widely used, is the rectangle.  
For example, the following code defines a simple rectangle with a light green
background, a dark green border, and padding values that everything inside the
shape must adhere to:

res/drawable/shape_green_rect.xml

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
<?xml version="1.0" encoding="utf-8"?>
<shape
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">
    <!-- Specify a semi-transparent solid green background color -->
    <solid android:color="#5500FF66" />
    <!-- Specify a dark green border -->
    <stroke 
        android:width="5dp"
        android:color="#009933" />
    <!-- Specify the margins that all content inside the drawable must adhere to -->
    <padding
        android:left="30dp"
        android:right="30dp"
        android:top="30dp"
        android:bottom="30dp" />
</shape>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Now you can reference that drawable just as you would any other drawable. In xml
it would be referenced as "\@drawable/shape_green_rect" and in code it would be
referenced as "R.drawable.shape_green_rect."

The following screenshot shows the above drawable used as a background to a
RelativeLayout that contains a single TextView element. Notice that there is a
nice distance between the text and the edge of the screen... That is controlled
by the padding value of the drawable because the TextView is inside the
RelativeLayout. Try changing the padding values (or taking them out altogether)
to see how the text positioning changes.

![](file:///D:/Mohsin/assets/assets/img/drawables.png)

Here is an example of another rectangle drawable... This one has a gradient
background and rounded corners. Note that even though I specify the radius for
the rounded corners individually, you can use the android:radius attribute to
specify that all corners should have the same radius:

res/drawable/shape_rounded_blue_rect.xml

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
<?xml version="1.0" encoding="utf-8"?>
<shape
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">
    <!-- Specify a gradient for the background -->
    <gradient
        android:angle="90"
        android:startColor="#55000066"
        android:centerColor="#FFFFFF"
        android:endColor="#55000066" />
    <!-- Specify a dark blue border -->
    <stroke 
        android:width="2dp"
        android:color="#000066" />
    <!-- Specify the margins that all content inside the drawable must adhere to -->
    <padding
        android:left="5dp"
        android:right="5dp"
        android:top="5dp"
        android:bottom="5dp" />
    <corners
        android:topLeftRadius="10dp"
        android:topRightRadius="10dp"
        android:bottomLeftRadius="10dp"
        android:bottomRightRadius="10dp" />
</shape>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Below are two screenshots that use a drawable with a gradient background on a
TextView. The one on the left is using the drawable xml from above. The XML for
the image on the right is not in this post but it gives you an idea of the
different effects you can apply to your views. (Note: You can download the
project that contains all the files at the end of this post):  
  


![](file:///D:/Mohsin/assets/assets/img/drawables1.png)

  
  


![](file:///D:/Mohsin/assets/assets/img/drawables2.png)

 

**Oval**
--------

  
  
The oval shape doesn't have any special tags... It only uses the tags common to
all shapes. Nevertheless, this shape can come in handy (though personally I've
never used it)...

So, let's have some fun with these shapes... I'm not really trying to make them
look good, just throwing some things together to show what you can do.

We'll take the following screenshot as our example... There are four different
oval XML files in use here and they all show off different things:

![](file:///D:/Mohsin/assets/assets/img/drawables3.png)

res/drawable/shape_oval_yellow.xml

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
<?xml version="1.0" encoding="utf-8"?>
<shape
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="oval">
    <gradient 
        android:type="radial"
        android:gradientRadius="20"
        android:centerX=".6"
        android:centerY=".35"
        android:startColor="#FFFF00"
        android:endColor="#FFFF99" />
    <size 
        android:width="100dp"
        android:height="100dp"/>
</shape>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This shows off the use of the radial gradient. It is important to note that if
you are using a radial gradient you must specify the gradientRadius attribute or
you will get a crash.

It also shows a use of the size tag... In my layout file I used
\@drawable/shape_oval_yellow as the background of an ImageView that has a width
and height of wrap_content. Since I am using an ImageView and there is nothing
inside of the drawable to define its size, the yellow circle would not have
shown up in the UI if I didn't specify the size. Alternatively I could have
specified a size other than wrap_content in the ImageView. Depending on what you
are trying to accomplish one way may end up working out better for you than the
other.

For example, if you don't specify the size in the drawable, then you could you
the same drawable over and over and give it different sizes every time you used
it. This would also be beneficial if you wanted to have the shape serve as a
background for a TextView... that way the size of the text would define the size
of your shape. But if you know you are always going to want images of a specific
size then you would want to define that in the drawable itself.

res/drawable/shape_oval_blue.xml

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
<?xml version="1.0" encoding="utf-8"?>
<shape
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="oval">
    <solid android:color="#0000FF" /> 
    <size 
        android:width="30dp"
        android:height="30dp"/> 
    <stroke
        android:dashWidth="3dp"
        android:dashGap="3dp"
        android:width="2dp"
        android:color="#0000FF" />
</shape>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This shape is used in two different ImageViews, each one using a different
rectangle shape as the background drawable and using this blue circle as the
foreground drawable. I did this to demonstrate the use of padding... The blue
rectangle shape only has a padding of 5dp on all sides while the green one has a
padding value of 30dp on all sides. Since the foreground drawable is considered
to be inside the background drawable, it adheres to the padding values specified
by the rectangle drawables.

I realized there is nothing really remarkable about this file, so I have decided
to omit it from this post. We have already seen everything this file is doing. .

/res/drawable/shape_oval_purple_gradient.xml

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
<?xml version="1.0" encoding="utf-8"?>
<shape
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="oval">
    <gradient 
        android:type="sweep"
        android:startColor="#77990099"
        android:endColor="#22990099"/>
    <stroke
        android:width="1dp"
        android:color="#aa990099" />
    <padding
        android:left="10dp"
        android:right="10dp"
        android:top="10dp"
        android:bottom="10dp" />
</shape>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This last oval is used as the background of a TextView so I decided not to
specify the size. If I change the text in the TextView then the size of the oval
will automatically adjust. It also demonstrates the use of a sweep-style
gradient.
