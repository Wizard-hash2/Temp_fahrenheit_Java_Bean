## GROUP WORK ; MEMBERS:
1. Haron kipsang Ngetich P01/0335/2023
2. Aron Kipkurui Ngeno P01/0713/2023
3. John Kamau P01/0310/2023
4. Malcolm Marenga Njoroge P01/0006/2022
5. Joseph Micubu Muirungi P01/0016/2022


# ComponentP — Temperature Converter (Java / JSP)

This is our school project which contains a few JavaBeans, a Swing GUI, an HTML form and a JSP page demonstrating temperature conversions between Celsius and Fahrenheit. 

## Summary

- Purpose: simple temperature conversion examples using JavaBeans: a Swing GUI app and a JSP-backed web form.
- Recommended way to run: open the project in NetBeans  and run the GUI or deploy the JSP to a servlet container (Apache Tomcat).

## Files and what they do

- `Java_Beans.java` (package `tbean`) — A serializable Java bean with `celsius` and `fahrenheit` properties and conversion methods `convertCelsiusToFahrenheit()` and `convertFahrenheitToCelsius()`.
- `TempBean.java` (package `com.mycompany.tempconvertergui`) — Another bean implementation with automatic updates (setting C updates F and vice-versa) and a `toString()` helper.
- `TempConverterGUI.java` — A Swing GUI (JFrame) with a text field, two radio buttons (C→F and F→C) and a Convert button. It reads the numeric input, uses a bean to convert, and shows a JOptionPane with the result. Run this class to launch the desktop converter.
- `Temp_Applet.java` —  applet variant of the converter.
- `newhtml.html` — A small HTML form that posts `tempValue` and `mode` to `test.jsp`.
- `test.jsp` — A JSP page that expects a JavaBean (the page uses `<jsp:useBean id="converter" class="com.mycompany.TemperatureConverter" scope="page" />`) and displays conversion results. Note: the JSP refers to a bean class `com.mycompany.TemperatureConverter` which is not present in the repository; see "Notes & fixes" below.

## run instructions 

1. Open the folder `ComponentP` in NetBeans (or import as a Java project). NetBeans will handle package dirs and classpath.
2. To run the desktop GUI: locate and run `TempConverterGUI` (it has a `main()` that launches the JFrame). Use the GUI to enter a value and choose conversion direction.
3. To use the JSP flow:
	 - Deploy the project or the relevant files to a servlet container (Tomcat).
	 - Make sure the bean class referenced by `test.jsp` exists on the classpath (see "Notes & fixes" below).
	 - Open `newhtml.html` in a browser (or navigate to it on the server), submit a value and view the result page.





## QUESTIONA :
1) Why is it a component
   Encapsulated functionality — AdderBean and AdderEjb each package a single responsibility (adding two numbers). That makes them reusable building blocks (components).
   Clear interface — they expose a small, well-defined API:
   AdderBean → properties setA(int)/setB(int) and getSum()
   AdderEjb → method add(int a,int b)
   Container-manageable — the JavaBean is usable by JSP/servlet containers; the EJB is managed by a Jakarta EE server (lifecycle, pooling, concurrency, security).
   Testable & replaceable — implementation is isolated so you can swap in another implementation or mock it in tests.
   Low coupling — callers only need the public methods; they don’t depend on internal state or UI logic.
2) How it’s accessed / interfaced with the web or package

The core conversion logic lives in JavaBean class(es) placed in a shared package, which act as the single source of truth and are imported or referenced by all interfaces.

On the web side, newhtml.html posts user input to test.jsp, which obtains the bean (for example via <jsp:useBean id="converter" class="com.mycompany.TemperatureConverter" scope="page" />), sets properties, calls the conversion methods, and renders the result.

The desktop Swing UI (TempConverterGUI) directly imports the bean package, calls its setters and conversion methods, and displays results in the GUI — showing the same component used in a non-web client.

A  applet can instantiate or delegate to the same bean to expose conversion services remotely , enabling server-side integration or transactional behaviour.

By keeping the bean API stable and ceolocated in one package, all layers (JSP, servlets, GUI, applet, backend) can reuse the component without duplicating logic



3) Where else can it be used (concrete examples)
Websites:

Weather dashboard — use the bean to let users toggle units and display temperatures consistently across pages and APIs.

Educational science portal — power interactive pages or exercises that demonstrate unit conversion and accept user input via forms or REST calls.
Packages / modules:

com.mycompany.reporting — reuse the bean to normalise temperature values before generating reports (PDF, CSV) so exported data uses consistent units.

com.mycompany.devices — use the bean in an IoT/sensor integration module to convert sensor readings into a canonical unit for storage and analysis.

# IMAGES
![APPLET](ComponentP\Temp_Applet.png)

![bean](ComponentP\Temp_Bean.png)

![EJB](ComponentP\Temp_EJB.png)

![GUI](ComponentP\Temp_GUI.png)