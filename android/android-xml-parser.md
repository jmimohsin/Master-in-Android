**Xml parser Example**
======================

The following is a valid, well-formated XML file.

```xml
<?xml version="1.0"?>
<address>
<name>Lars </name>
<street> Test </street>
<telephon number= "0123"/>
</address>
```

The Java programming language provides several standard libraries for processing
XML files. The SAX and the DOM XML parsers are also available on Android.  
The SAX and DOM parsers API is on Android the same as in standard Java. SAX and
DOM have their limitations, therefore it is not recommended to use them on
Android. Therefore this tutorial does not give an example for the usage of this
library.  
The Java standard provides also the Stax parser. This parser is not part of the
Android platform.  
Android provides for XML parsing and writing the XmlPullParser class. This
parser is not available in standard Java but is similar to the Stax parser. The
parser is hosted at http://www.xmlpull.org/ .  
On Android it is recommended to use the XmlPullParser. It has a relatively
simple API compared to SAX and DOM and is fast and requires less memory then the
DOM API.

```java
import java.io.IOException;
import java.io.StringReader;
import org.xmlpull.v1.XmlPullParser;
import org.xmlpull.v1.XmlPullParserException.html;
import org.xmlpull.v1.XmlPullParserFactory;
public class SimpleXmlPullApp {
public static void main (String args[]) throws XmlPullParserException, IOException {
XmlPullParserFactory factory = XmlPullParserFactory.newInstance();
factory.setNamespaceAware(true);
XmlPullParser xpp = factory.newPullParser();
xpp.setInput(new StringReader ("Hello World!"));
int eventType = xpp.getEventType();
while (eventType != XmlPullParser.END_DOCUMENT) {
if(eventType == XmlPullParser.START_DOCUMENT) {
System.out.println("Start document");
} else if(eventType == XmlPullParser.END_DOCUMENT) {
System.out.println("End document");
} else if(eventType == XmlPullParser.START_TAG) {
System.out.println("Start tag "+xpp.getName());
} else if(eventType == XmlPullParser.END_TAG) {
System.out.println("End tag "+xpp.getName());
} else if(eventType == XmlPullParser.TEXT) {
System.out.println("Text "+xpp.getText());
}
eventType = xpp.next();
}
}
}
```
