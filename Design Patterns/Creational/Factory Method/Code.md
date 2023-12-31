## Question
You are tasked with designing a document processing application that can export documents to various formats, such as PDF, DOCX, and HTML. Implement the Factory Method design pattern to create a DocumentExporter framework that allows for the creation of specific document exporter objects based on the desired output format. Provide a class diagram and explain how the Factory Method pattern supports the extensibility of the application for adding new document export formats.

In your response, describe the roles and responsibilities of each class involved in the Factory Method pattern and how it enables the application to handle different output formats with ease. Discuss how this design pattern allows for the addition of new document export formats without modifying existing code and any potential advantages or drawbacks of this approach.

## UML :
![Screenshot 2023-09-06 at 10 39 23 PM](https://github.com/SiddharthMathurDeveloper/Backend-Engineering/assets/133037456/9f2ed160-fd5f-4160-8250-9149fe2c6149)



## Code :

### Client.java
```java
public class Client {
    public static void main(String[] args) {
        document(new DocxDocumentCreator());
    }

    public  static  void document(DocumentCreator documentCreator){
        DocumentExporter exporter = documentCreator.getDocumentExporter();

        exporter.changeToExport();
        exporter.renameFileName();
    }
}
```

### DocumentCreator.java
```java
public abstract class DocumentCreator {

    public DocumentExporter getDocumentExporter(){
        DocumentExporter documentExporter = createDocumentExporter();
       

        return documentExporter;
    }

    protected abstract DocumentExporter createDocumentExporter();
}
```


### PdfDocumentCreator.java
```java
public class PdfDocumentCreator extends DocumentCreator {
    @Override
    protected DocumentExporter createDocumentExporter() {
        return new PdfDocumentExporter();
    }
}
```

### DocxDocumentCreator.java
```java
public class DocxDocumentCreator extends DocumentCreator{
    @Override
    protected DocumentExporter createDocumentExporter() {
        return new DocxDocumentExporter();
    }
}


```









### DocumentExporter.java
```java
public interface DocumentExporter {
    void changeToExport();
    void renameFileName();
}
```


### PdfDocumentExporter.java
```java
public class PdfDocumentExporter implements DocumentExporter {

    @Override
    public void changeToExport() {
        System.out.println("Change to PDF Version");
    }

    @Override
    public void renameFileName() {
        System.out.println("renamed this PDF file to anything");
    }
}
```


### DocxDocumentExporter.java
```java
public class DocxDocumentExporter implements DocumentExporter {
    @Override
    public void changeToExport() {
        System.out.println("Change to Docx Version");
    }

    @Override
    public void renameFileName() {
        System.out.println("renamed this docx file to anything");
    }
}
```






