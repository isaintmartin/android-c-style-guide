#Moove-it Android-c-style-guide

# Table of Contents
  * [Sapacing](#spacing)
  * [Conditionals](#conditionals)
  * [Error Handling] (#error_handling)
  * [Naming] (#naming)
  
##Sapacing <a id="spacing"></a>
* Ident using 4 spaces. Never use tabs.
* Ident using 8 spaces for line wraps, including function calls and assignments.

**For example:**

```
Instrument i =
        someLongExpression(that, wouldNotFit, on, one, line);
```

**Not:**

```
Instrument i =
    someLongExpression(that, wouldNotFit, on, one, line);
```

* There should be exactly one blank line between methods to aid in visual clarity and organization.
* Braces do not go on their own line, they go on the same line as the code before them.

**For example:**

```
class MyClass {
    int func() {
        if (something) {
            // ...
        } else {
            // ...
        }
    }
}
```

**Not:**

```
class MyClass 
{
    int func() 
    {
        if (something) 
        {
            // ...
        } 
        else 
        {
            // ...
        }
    }
}
```

##Conditionals <a id="conditionals"></a>

Conditional bodies should always use braces even when a conditional body could be written without braces (e.g., it is one line only) to prevent errors. These errors include adding a second line and expecting it to be part of the if-statement. Another defect may happen where the line “inside” the if-statement is commented out, and the next line unwittingly becomes part of the if-statement. In addition, this style is more consistent with all other conditionals, and therefore more easily scannable.

**For example:**

```
if (!error) {
    return success;
}
```

**Not:**

```
if (!error)
    return success;
```

##Error Handling <a id="error_handling"></a>

* Don't Ignore Exceptions.  You must handle every Exception in your code in some principled way. The specific handling varies depending on the case.

**For example:**

* Throw the exception up to the caller of your method.

```
void setServerPort(String value) throws NumberFormatException {
    serverPort = Integer.parseInt(value);
}
```

* Throw a new exception that's appropriate to your level of abstraction.

```
void setServerPort(String value) throws ConfigurationException {
    try {
        serverPort = Integer.parseInt(value);
    } catch (NumberFormatException e) {
        throw new ConfigurationException("Port " + value + " is not valid.");
    }
}
```
**Not:**

* Ignore exception

```
void setServerPort(String value) {
    try {
        serverPort = Integer.parseInt(value);
    } catch (NumberFormatException e) { }
}
```

* Catch generic exception

```
try {
    someComplicatedIOFunction();        // may throw IOException 
    someComplicatedParsingFunction();   // may throw ParsingException 
    someComplicatedSecurityFunction();  // may throw SecurityException 
    // phew, made it all the way 
} catch (Exception e) {                 // I'll just catch all exceptions 
    handleError();                      // with one generic handler!
}
```

##Naming <a id="naming"></a>

###General
* Non-public, non-static field names start with m.
* Static field names start with s.
* Other fields start with a lower case letter.
* Public static final fields (constants) are ALL_CAPS_WITH_UNDERSCORES.
* Long, descriptive method and variable names are good.

**For example:**

```
public class MyClass {
    public static final int SOME_CONSTANT = 42;
    public int publicField;
    private static MyClass sSingleton;
    int mPackagePrivate;
    private int mPrivate;
    protected int mProtected;
}
```

**Not:**

```
public class MyClass {
    public int pubField;
    int mPackPriv;
}
```
###Activities and Fragments
* Java class: Description of the activity and the word *Activity* 
* Layout: The word *Activity* followed by underscore and the description of the activity
* The same criteria is used for Fragments
* General layouts: The word *layout* followed by underscore and the description of the layout
* Drawables: Always define with the prefix *dw*

**For example:**

```
LoginActivity.java 
activity_login.xml
layout_list_item_asset.xml
dw_rounded_button_blue.xml
```

