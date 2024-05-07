# Notes
Product:
```java
public interface GUI {}

public class Button implements GUI {}

public class Checkbox implements GUI {}
```

Factory:
```java
public interface GUIFactory {
    GUI create();
}

public class ButtonFactory implements GUIFactory {
    @Override
    public GUI create() {
        return new Button();
    }
}

public class CheckboxFactory implements GUIFactory {
    @Override
    public GUI create() {
        return new Checkbox();
    }
}
```

Usage:
```java
ButtonFactory buttonFactory = new ButtonFactory();
CheckboxFactory checkboxFactory = new CheckboxFactory();

List<GUI> guis = new ArrayList<>();
guis.add(buttonFactory.create());
guis.add(checkboxFactory.create());
```
