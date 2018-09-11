**Android Styles and Themes**
=============================

If you already know about Cascading Style Sheet (CSS) in web design then to
understand Android Style also works very similar way. There are number of
attributes associated with each Android widget which you can set to change your
application look and feel. A style can specify properties such as height,
padding, font color, font size, background color, and much more.

You can specify these attributes in Layout file as follows:
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
   android:layout_width="fill_parent"
   android:layout_height="fill_parent"
   android:orientation="vertical" >
 
   <TextView
   android:id="@+id/text_id"
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"
   android:capitalize="characters"
   android:textColor="#00FF00"
   android:typeface="monospace"
   android:text="@string/hello_world" />
 
</LinearLayout>
```

 

But this way we need to define style attributes for every attribute separately
which is not good for source code maintenance point of view. So we work with
styles by defining them in separate file as explained below.

 

**Defining Styles**
-------------------

A style is defined in an XML resource that is separate from the XML that
specifies the layout. This XML file resides under **res/values/** directory of
your project and will have **\<resources\>** as the root node which is mandatory
for the style file. The name of the XML file is arbitrary, but it must use the
.xml extension.

You can define multiple styles per file using **\<style\>** tag but each style
will have its name that uniquely identifies the style. Android style attributes
are set using **\<item\>** tag as shown below:

 

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
   <style name="CustomFontStyle">
      <item name="android:layout_width">fill_parent</item>
      <item name="android:layout_height">wrap_content</item>
      <item name="android:capitalize">characters</item>
      <item name="android:typeface">monospace</item>
      <item name="android:textSize">12pt</item>
      <item name="android:textColor">#00FF00</item>/>
   </style>
</resources>
```
 

The value for the \<item\> can be a keyword string, a hex color, a reference to
another resource type, or other value depending on the style property.

 

**Using Styles**
----------------

Once your style is defined, you can use it in your XML Layout file using
**style** attribute as follows:

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
   android:layout_width="fill_parent"
   android:layout_height="fill_parent"
   android:orientation="vertical" >
 
   <TextView
   android:id="@+id/text_id"
   style="@style/CustomFontStyle"
   android:text="@string/hello_world" />
 
</LinearLayout>
```

 

To understand the concept related to Android Style, you can check Style Demo
Example.

 

**Style Inheritance**
---------------------

Android supports style Inheritance in very much similar way as cascading style
sheet in web design. You can use this to inherit properties from an existing
style and then define only the properties that you want to change or add.

Its simple, to create a new style **LargeFont** that inherits the
**CustomFontStyle** style defined above, but make the font size big, you can
author the new style like this:

 

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
   <style name="CustomFontStyle.LargeFont">
      <item name="android:textSize">20ps</item>
   </style>
</resources>
```

 

You can reference this new style as **\@style/CustomFontStyle.LargeFont** in
your XML Layout file. You can continue inheriting like this as many times as
you'd like, by chaining names with periods. For example, you can extend
FontStyle.LargeFont to be Red, with:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
   <style name="CustomFontStyle.LargeFont.Red">
      <item name="android:textColor">#FF0000</item>/>
   </style>
</resources>
```

This technique for inheritance by chaining together names only works for styles
defined by your own resources. You can't inherit Android built-in styles this
way. To reference an Android built-in style, such as **TextAppearance**, you
must use the **parent** attribute as shown below:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
   <style name="CustomFontStyle" parent="@android:style/TextAppearance">
      <item name="android:layout_width">fill_parent</item>
      <item name="android:layout_height">wrap_content</item>
      <item name="android:capitalize">characters</item>
      <item name="android:typeface">monospace</item>
      <item name="android:textSize">12pt</item>
      <item name="android:textColor">#00FF00</item>/>
   </style>
</resources>
```
Hope you understood the concept of Style, so now let's try to understand what is
a **Theme**. A theme is nothing but an Android style applied to an entire
Activity or application, rather than an individual View.

Thus, when a style is applied as a theme, every **View** in the Activity or
application will apply each style property that it supports. For example, you
can apply the same **CustomFontStyle** style as a theme for an Activity and then
all text inside that **Activity** will have green monospace font.

To set a theme for all the activities of your application, open the
**AndroidManifest.xml** file and edit the **\<application\>** tag to include the
**android:theme** attribute with the style name. For example:

```xml
<application android:theme="@style/CustomFontStyle">
```

But if you want a theme applied to just one Activity in your application, then
add the android:theme attribute to the \<activity\> tag only. For example:

```xml
<activity android:theme="@style/CustomFontStyle">
```

There are number of default themes defined by Android which you can use directly
or inherit them using **parent** attribute as follows:

```xml
<style name="CustomTheme" parent="android:Theme.Light">
    ...
</style>
```

To understand the concept related to Android Theme, you can check Theme Demo
Example.

**Default Styles & Themes**
---------------------------

The Android platform provides a large collection of styles and themes that you
can use in your applications. You can find a reference of all available styles
in the **R.style** class. To use the styles listed here, replace all underscores
in the style name with a period. For example, you can apply the Theme_NoTitleBar
theme with "\@android:style/Theme.NoTitleBar". You can see the following source
code for Android styles and themes:

-   Android Styles (styles.xml)

-   Android Themes (themes.xml)
