# Chapter 5: Formatting

```text
Don't write the code like drunken sailors
```

### The Purpose of Formatting

- Code formatting is about communication, and communication is the professional developer's first order of business .

### Vertical Formatting

- The number of lines in file it should be around 200 ~ 500 and as much making them small

### The Newspaper Metaphor 

- Make the file resemble a newspaper by including `headlines` to describe its purpose and content, instead of  using the file name or comments.

### Vertical Openness Between Concepts 

- Add `blank lines` to spreate the concepts like lines between declaration of functions .
#### It's better to write it in this way:

```java
package fitnesse.wikitext.widgets;

import java.util.regex.*;

public class BoldWidget extends ParentWidget {
    public static final String REGEXP = "'''.+?'''";
    private static final Pattern pattern = Pattern.compile("'''(.+?)'''", Pattern.MULTILINE + Pattern.DOTALL );

    public BoldWidget(ParentWidget parent, String text) throws Exception { 
    super(parent);
    Matcher match = pattern.matcher(text);  
    match.find();
    addChildWidgets(match.group(1)); 
    }
    
    public String render() throws Exception { 
    StringBuffer html = new StringBuffer("<b>"); html.append(childHtml()).append("</b>"); return html.toString();
    }
}
```

### Vertical Density
- If openness separates concepts, then vertical density implies close association. So lines of code that are tightly related should appear vertically densely
#### Don't do that :

```java
public class ReporterConfig {
    /**
    * The class name of the reporter listener */
    private String m_className;
    /**
    *The properties of the reporter listener */
    private List<Property> m_properties = new ArrayList<Property>();

    public void addProperty(Property property) {
        m_properties.add(property);
    }
}
```
#### It's better to write it in this way:

```java
public class ReporterConfig {

    private String m_className;
    private List<Property> m_properties = new ArrayList<Property>();

    public void addProperty(Property property) {
        m_properties.add(property);
    }
}
```

### Vertical Distance
- Make all concepts that are `closely related` in verticall close to each other
- That not working with for concepts that belong in sparate file we should avoid separet concepts as much as can 

### Variable Declarations
- `Local variables` should delceler on the top of function .
- `Control variables` for loops should usually be declared within the loop statement

### Instance variables
- can decleare in top of class like java or bottom like c++ any thing else is strange 

### Dependent Functions
- decleare caller on top of callee

### Conceptual Affinity
- Group all concepts that like each other in vertical close to each other like overloading .
#### like that :
```java 
public class Assert {
    static public void assertTrue(String message, boolean condition) {
        if (!condition) fail(message);
    }
    static public void assertTrue(boolean condition) { 
        assertTrue(null, condition);
    }
    static public void assertFalse(String message, boolean condition) {
        assertTrue(message, !condition);
    }
    static public void assertFalse(boolean condition) {
        assertFalse(null, condition);
    }
}
```
### Vertical Ordering
- like Dependent Functions

### Horizontal Formatting
- The width of line must be limit 120 charchater 


### Horizontal Openness and Density
- Add space  
    - between paramter name and type
    - between any keywords
    - space after comma 
    - space after parenthesis and calry bracket 
    -  accentuate the precedence of operator
- Don't put space 
    - between function name and 
    - between  bracket and wat after or before
    - end of paramter and comma 
    - same comma and what berfor it 

#### Like this :
```java 
public class Quadratic {
    public static double root1(double a, double b, double c) {
        double determinant = determinant(a, b, c);
        return (-b + Math.sqrt(determinant)) / (2*a); 
    }
    public static double root2(int a, int b, int c) {
        double determinant = determinant(a, b, c);
        return (-b - Math.sqrt(determinant)) / (2*a);
    }
    private static double determinant(double a, double b, double c) {
        return b*b - 4*a*c;
    } 
}
```
    
### Horizontal Alignment
#### don't do that:
```java
public class FitNesseExpediter implements ResponseSender {
    private   Socket          socket;
    private   InputStream     input;
    private   OutputStream    output;
    private   Request         request;
    protected Response        response;
    private   FitNesseContext context;
    public FitNesseExpediter(Socket s, FitNesseContext context) throws Exception {
        this.context =  context;
        socket =        s;
        input =         s.getInputStream();
    }
}
```
#### It's better to write it in this way:
```java
public class FitNesseExpediter implements ResponseSender {
    private Socket socket;
    private InputStream input;
    private OutputStream output;
    private Request request;
    protected Response response;
    private FitNesseContext context;
    public FitNesseExpediter(Socket s, FitNesseContext context) throws Exception {
        this.context = context;
        socket = s;
        input = s.getInputStream();
    }
}
```
### Indentation
```text
spacing at the beginning of lines of code
```
- make file like hierarchy order 
#### like that
```java 

public class FitNesseServer implements SocketServer { //no spacing on beginning
    private FitNesseContext context; //one tab on beginning
    public FitNesseServer(FitNesseContext context) { //one tab on beginning
        this.context = context; //two tab on beginning
    } 
    public void serve(Socket s) {
        serve(s, 10000); 
    } 
    public void serve(Socket s, long requestTimeout) {
        try { //two tab on beginning
            FitNesseExpediter sender = new FitNesseExpediter(s, context); //three tab on beginning
            sender.setRequestParsingTimeLimit(requestTimeout);
            sender.start();
        } 
        catch(Exception e) {
            e.printStackTrace(); 
        } 
    } 
}
```

### Don't Breaking Indentation
```text 
Don't write for , if , while or any thing have block on single line 
```
#### don't do that:
```java
public class CommentWidget extends TextWidget {
    public static final String REGEXP = "^#[^\r\n]*(?:(?:\r\n)|\n|\r)?";
    public CommentWidget(ParentWidget parent, String text) {super(parent, text);}
    public String render() throws Exception {return "";} 
}
```
#### It's better to write it in this way:
```java
public class CommentWidget extends TextWidget {
    public static final String REGEXP = "^#[^\r\n]*(?:(?:\r\n)|\n|\r)?";
    
    public CommentWidget(ParentWidget parent, String text) {
        super(parent, text);
    }
    
    public String render() throws Exception {
        return "";
    } 
}
```


### Dummy Scopes 
#### Don't do that:
```java
while (dis.read(buf, 0, readBufferSize) != -1)
;
```

### Team Rules
``` text
we should as team agree on one style we will apply on whole the project
```
### Uncle Bob’s Formatting Rules
``` java
public class CodeAnalyzer implements JavaFileAnalysis {
    private int lineCount;
    private int maxLineWidth;
    private int widestLineNumber;
    private LineWidthHistogram lineWidthHistogram;
    private int totalChars;
    
    public CodeAnalyzer() {
        lineWidthHistogram = new LineWidthHistogram();
    }
    
    public static List<File> findJavaFiles(File parentDirectory) {
        List<File> files = new ArrayList<File>();
        findJavaFiles(parentDirectory, files);
        return files;
    }
    private static void findJavaFiles(File parentDirectory, List<File> files) {
        for (File file : parentDirectory.listFiles()) {
            if (file.getName().endsWith(".java")) 
                files.add(file);
            else if (file.isDirectory()) 
                findJavaFiles(file, files); 
        }
    }
    
    public void analyzeFile(File javaFile) throws Exception { 
        BufferedReader br = new BufferedReader(new FileReader(javaFile));
        String line;
        while ((line = br.readLine()) != null) {
            measureLine(line); 
        }
    }
    
    private void measureLine(String line) { 
        lineCount++;
        int lineSize = line.length();
        totalChars += lineSize;
        lineWidthHistogram.addLine(lineSize, lineCount);
        recordWidestLine(lineSize);
    }
    
    private void recordWidestLine(int lineSize) {
        if (lineSize > maxLineWidth) {
            maxLineWidth = lineSize;
            widestLineNumber = lineCount; 
        }
    }
    
    public int getLineCount() { 
        return lineCount;
    }
    public int getMaxLineWidth() { 
        return maxLineWidth;
    }
    
    public int getWidestLineNumber() { 
        return widestLineNumber;
    }
    
    public LineWidthHistogram getLineWidthHistogram() { 
        return lineWidthHistogram;
    }
    
    public double getMeanLineWidth() { 
        return (double)totalChars/lineCount;
    }
    
    public int getMedianLineWidth() {
        Integer[] sortedWidths = getSortedWidths();
        int cumulativeLineCount = 0;
        for (int width : sortedWidths) {
            cumulativeLineCount += lineCountForWidth(width);
            if (cumulativeLineCount > lineCount/2) 
                return width;
        }
        throw new Error("Cannot get here"); 
    }
    
    private int lineCountForWidth(int width) {
        return lineWidthHistogram.getLinesforWidth(width).size();
    }

    private Integer[] getSortedWidths() {
        Set<Integer> widths = lineWidthHistogram.getWidths();
        Integer[] sortedWidths = (widths.toArray(new Integer[0])); Arrays.sort(sortedWidths);
        return sortedWidths;
    } 
}
```

