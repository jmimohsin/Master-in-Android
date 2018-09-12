**XML SAX Parser**
==================

This Android example shows how to parse a simple XML containing employee details
using SAX parser and display the result in Spinner.  
  
This example stores XML file in project’s assets folder and opens the file as
InputStream using AssetManager.  
  
On button click event, we parse the XML and display employee id and name in
Spinner and when an item is selected, complete employee detail is displayed in a
Toast message.

To parse an XML in Android, you can use DOM and SAX parser API provided by Java
platform. In addition to these two parsers, Android provides XmlPullParser which
is similar to StAX parser and is also the recommended parser to use in Android.

**Create XML file**
-------------------

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
<?xml version="1.0" encoding="UTF-8"?>
<employees>
    <employee>
        <id>2163</id>
        <name>Kumar</name>
        <department>Development</department>
        <type>Permanent</type>
        <email>kumar@tot.com</email>
    </employee>
    <employee>
        <id>6752</id>
        <name>Siva</name>
        <department>DB</department>
        <type>Contract</type>
        <email>siva@tot.com</email>
    </employee>
    <employee>
        <id>6763</id>
        <name>Timmy</name>
        <department>Testing</department>
        <type>Permanent</type>
        <email>timmy@tot.com</email>
    </employee>
</employees>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Main layout file** 
---------------------

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:padding="10dip"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content">
    <Button
    android:id="@+id/button"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    android:text="@string/button" />

    <Spinner
    android:id="@+id/spinner"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    />
</LinearLayout>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Employee.java**<br>
---------------------

Create a new Java class “Employee.java” in package
“com.theopentutorials.android.beans” and copy the following code.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
public class Employee {
    private String name;
    private int id;
    private String department;
    private String type;
    private String email;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getId() {
        return id;
    }
    public void setId(int id) {
        this.id = id;
    }
    public String getDepartment() {
        return department;
    }
    public void setDepartment(String department) {
        this.department = department;
    }
    public String getType() {
        return type;
    }
    public void setType(String type) {
        this.type = type;
    }
    public String getEmail() {
        return email;
    }
    public void setEmail(String email) {
        this.email = email;
    }
    @Override
    public String toString() {
        return id + ": " + name;
    }
    public String getDetails() {
        String result = id + ": " + name + "\n" + department + "-" + type + "\n" + email;
        return result;
    }
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Create SAXXMLHandler class**
------------------------------

Create a new Java class “SAXXMLHandler.java” in package
“com.theopentutorials.android.xml” and copy the following code.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
public class SAXXMLHandler extends DefaultHandler {
    private List<Employee> employees;
    private String tempVal;
    private Employee tempEmp;

    public SAXXMLHandler() {
        employees = new ArrayList<Employee>();
    }
    public List<Employee> getEmployees() {
        return employees;
    }
    // Event Handlers
    public void startElement(String uri, String localName, String qName, Attributes attributes) throws SAXException {
        // reset
        tempVal = "";
        if (qName.equalsIgnoreCase("employee")) {
            // create a new instance of employee
            tempEmp = new Employee();
        }
    }
    public void characters(char[] ch, int start, int length)
    throws SAXException {
        tempVal = new String(ch, start, length);
    }
    public void endElement(String uri, String localName, String qName)
    throws SAXException {
        if (qName.equalsIgnoreCase("employee")) {
            // add it to the list
            employees.add(tempEmp);
        } else if (qName.equalsIgnoreCase("id")) {
            tempEmp.setId(Integer.parseInt(tempVal));
        } else if (qName.equalsIgnoreCase("name")) {
            tempEmp.setName(tempVal);
        } else if (qName.equalsIgnoreCase("department")) {
            tempEmp.setDepartment(tempVal);
        } else if (qName.equalsIgnoreCase("type")) {
            tempEmp.setType(tempVal);
        } else if (qName.equalsIgnoreCase("email")) {
            tempEmp.setEmail(tempVal);
        }
    }
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

SAX (Simple API for XML) is an event-based sequential access parser API with
number of callback methods that will be called when events like start element,
end element, attributes etc occur during parsing. This class parses a XML file
containing employee details and stores in a list as an employee object.

**Create SAXXMLParser class**
-----------------------------

Create a new Java class “SAXXMLParser.java” in package
“com.theopentutorials.android.xml” and copy the following code.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
public class SAXXMLParser {
    public static List<Employee> parse(InputStream is) {
        List<Employee> employees = null;
        try {
            // create a XMLReader from SAXParser
            XMLReader xmlReader = SAXParserFactory.newInstance().newSAXParser() .getXMLReader();
            // create a SAXXMLHandler
            SAXXMLHandler saxHandler = new SAXXMLHandler();
            // store handler in XMLReader
            xmlReader.setContentHandler(saxHandler);
            // the process starts
            xmlReader.parse(new InputSource(is));
            // get the `Employee list`
            employees = saxHandler.getEmployees();
        } catch (Exception ex) {
            Log.d("XML", "SAXXMLParser: parse() failed");
        }
        // return Employee list
        return employees;
    }
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Create SAXParserActivity class**
----------------------------------

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
public class MainActivity extends Activity implements
OnClickListener, OnItemSelectedListener {
    Button button;
    Spinner spinner;
    List<Employee> employees = null;
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        findViewsById();
        button.setOnClickListener(this);
    }
    private void findViewsById() {
        button = (Button) findViewById(R.id.button);
        spinner = (Spinner) findViewById(R.id.spinner);
    }
    public void onClick(View v) {
        try {
            employees = SAXXMLParser.parse(getAssets().open("employee.xml"));
            ArrayAdapter<Employee> adapter = new ArrayAdapter(this, android.R.layout.simple_list_item_1, employees);
            spinner.setAdapter(adapter);
            spinner.setOnItemSelectedListener(this);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    @Override
    public void onItemSelected(AdapterView parent, View view, int pos, long id) {
        Employee employee = (Employee) parent.getItemAtPosition(pos);
        Toast.makeText(parent.getContext(), employee.getDetails(), Toast.LENGTH_LONG).show();
    }
    @Override
        public void onNothingSelected(AdapterView arg0) {
    }
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Demo**
--------

![](file:///D:/Mohsin/assets/assets/img/sax1.png)

  
  


![](file:///D:/Mohsin/assets/assets/img/sax4.jpg)
