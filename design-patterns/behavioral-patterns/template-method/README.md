# Notes

## Demo from Refactoring Guru
```java
public interface DataMiner {
    default Report mineData(String path) {
        File file = openResource(path);
        Data data = extractData(file);
        Data processedData = processData(data);
        Analysis analysis = analyzeData(processedData);
        Report report = reportResults(analysis);
        closeResource(file);

        return report;
    }

    default File openResource(String path) {
        File file = new File(path);
        return file;
    }

    Data extractData(File file);

    Data processData(Data data);

    Analysis analyzeData(Data data);

    default Report reportResults(Analysis analysis) {
        return new Report(analysis);
    }

    default void closeResource(File file) {
        file.close();
    }
}

public class PDFDataMiner implements DataMiner {
    @Override
    public Data extractData(File file) {
        ...
    }

    @Override
    public Data processData(Data data) {
        ...
    }

    @Override
    public Analysis analyzeData(Data data) {
        ...
    }
}
```

Using abstract class instead of interface:
```java
public abstract DataMiner {
    public Report mineData(String path) {
        File file = openResource(path);
        Data data = extractData(file);
        Data processedData = processData(data);
        Analysis analysis = analyzeData(processedData);
        Report report = reportResults(analysis);
        closeResource(file);

        return report;
    }

    private File openResource(String path) {
        File file = new File(path);
        return file;
    }

    protected Data extractData(File file);

    protected Data processData(Data data);

    protected Analysis analyzeData(Data data);

    private Report reportResults(Analysis analysis) {
        return new Report(analysis);
    }

    private void closeResource(File file) {
        file.close();
    }
}

public class PDFDataMiner extends DataMiner {
    @Override
    protected Data extractData(File file) {
        ...
    }

    @Override
    protected Data processData(Data data) {
        ...
    }

    @Override
    protected Analysis analyzeData(Data data) {
        ...
    }
}
```

## Simplified Demo
```java
public interface RequestProcessor {
    void processRequest(RequestContext requestContext);

    default void validateAndProcessRequest(RequestContext requestContext) {
        if (RequestValidator.validateRequest(requestContext)) {
            processRequest(requestContext);
        }
    }
}

public class DepositRequestProcessor implements RequestProcessor {
    @Override
    public void processRequest(RequestContext requestContext) {
        ...
    }
}
```

## Complete Demo
```java
public interface RequestContext {}

public interface RequestValidator<T extends RequestContext> {
    boolean validateRequest(T requestContext);
}

public interface RequestProcessor<U extends RequestContext, V extends RequestValidator<U>> {
    void processRequest(U requestContext);

    default void validateAndProcessRequest(U requestContext, V requestValidator) {
        if (requestValidator.validateRequest(requestContext)) {
            processRequest(requestContext);
        }
    }
}
```
