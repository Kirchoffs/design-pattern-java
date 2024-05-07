# Notes
## Dispatch
- Static dispatch: the implementation of a polymorphic operation is determined at compile time.
- Dynamic dispatch: the implementation of a polymorphic operation is determined at runtime.

## Double Dispatch
- Single dispatch: the choice of which version of a method to call is based on a single object.
- Multiple dispatch: the choice of which version of a method to call is based on a combination if objects.
- Double dispatch: the choice of which version of a method to call is based on two objects.

More specifically, double dispatch involves selecting a method based on the runtime types of two objects: the receiver and the argument.

Languages such as Java, JavaScript, C++, and Python support only single dispatch polymorphism, where the method to be called is determined based on a single object. However, double dispatch can be simulated in these languages using the Visitor pattern.

```java
public interface Element {
    void accept(Visitor visitor);
}

public class AlphaElement implements Element {
    @Override
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}

public class BetaElement implements Element {
    @Override
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}
```

```java
public interface Visitor {
    default void visit(Element element) {
        element.accept(this);
    }

    void visit(AlphaElement element);
    void visit(BetaElement element);
}

public class FirstVisitor implements Visitor {
    @Override
    public void visit(AlphaElement element) {
        // do something with element
    }

    @Override
    public void visit(BetaElement element) {
        // do something with element
    }
}

public class SecondVisitor implements Visitor {
    @Override
    public void visit(AlphaElement element) {
        // do something with element
    }

    @Override
    public void visit(BetaElement element) {
        // do something with element
    }
}
```

```java
Element alphaElement = new AlphaElement();
Element betaElement = new BetaElement();

Visitor firstVisitor = new FirstVisitor();
Visitor secondVisitor = new SecondVisitor();

alphaElement.accept(firstVisitor);
alphaElement.accept(secondVisitor);
betaElement.accept(firstVisitor);
betaElement.accept(secondVisitor);

firstVisitor.visit(alphaElement);
firstVisitor.visit(betaElement);
secondVisitor.visit(alphaElement);
secondVisitor.visit(betaElement);
```

To create another new visitor (a new operator):
```java
public class ThirdVisitor implements Visitor {
    @Override
    public void visit(AlphaElement element) {
        // do something with element
    }

    @Override
    public void visit(BetaElement element) {
        // do something with element
    }
}
```
