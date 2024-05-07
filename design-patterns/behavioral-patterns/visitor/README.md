# Notes
Sometimes context is needed to be passed to the visitor. This can be done by passing the context to the accept method of the element and then passing it to the visit method of the visitor.

```java
public interface Element {
    void accept(Visitor visitor, Context context);
}

public class AlphaElement implements Element {
    @Override
    public void accept(Visitor visitor, Context context) {
        visitor.visit(this, context);
    }
}

public class BetaElement implements Element {
    @Override
    public void accept(Visitor visitor, Context context) {
        visitor.visit(this, context);
    }
}
```

```java
public interface Visitor {
    default void visit(Element element, Context context) {
        element.accept(this, context);
    }

    void visit(AlphaElement element, Context context);
    void visit(BetaElement element, Context context);
}

public class FirstVisitor implements Visitor {
    @Override
    public void visit(AlphaElement element, Context context) {
        // do something with element and context
    }

    @Override
    public void visit(BetaElement element, Context context) {
        // do something with element and context
    }
}

public class SecondVisitor implements Visitor {
    @Override
    public void visit(AlphaElement element, Context context) {
        // do something with element and context
    }

    @Override
    public void visit(BetaElement element, Context context) {
        // do something with element and context
    }
}
```

```java
Element alphaElement = new AlphaElement();
Element betaElement = new BetaElement();

Visitor firstVisitor = new FirstVisitor();
Visitor secondVisitor = new SecondVisitor();

Context context = new Context();

alphaElement.accept(firstVisitor, context);
alphaElement.accept(secondVisitor, context);
betaElement.accept(firstVisitor, context);
betaElement.accept(secondVisitor, context);

firstVisitor.visit(alphaElement, context);
firstVisitor.visit(betaElement, context);
secondVisitor.visit(alphaElement, context);
secondVisitor.visit(betaElement, context);
```

To create another new visitor (a new operator):
```java
public class ThirdVisitor implements Visitor {
    @Override
    public void visit(AlphaElement element, Context context) {
        // do something with element and context
    }

    @Override
    public void visit(BetaElement element, Context context) {
        // do something with element and context
    }
}
```
