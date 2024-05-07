# Notes
Product:
```java
public interface GUI {}

public interface Button extends GUI {}

public interface Checkbox extends GUI {}

public class WindowsButton implements Button {}

public class MacButton implements Button {}

public class WindowsCheckbox implements Checkbox {}

public class MacCheckbox implements Checkbox {}
```

Factory:
```java
public interface GUIFactory {
    Button createButton();
    Checkbox createCheckbox();
}

public class WindowsGUIFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new WindowsButton();
    }

    @Override
    public Checkbox createCheckbox() {
        return new WindowsCheckbox();
    }
}

public class MacGUIFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new MacButton();
    }

    @Override
    public Checkbox createCheckbox() {
        return new MacCheckbox();
    }
}
```

Usage:
```java
GUIFactory windowsGUIFactory = new WindowsGUIFactory();
GUIFactory macGUIFactory = new MacGUIFactory();

List<Button> buttons = new ArrayList<>();
buttons.add(windowsGUIFactory.createButton());
buttons.add(macGUIFactory.createButton());

List<Checkbox> checkboxes = new ArrayList<>();
checkboxes.add(windowsGUIFactory.createCheckbox());
checkboxes.add(macGUIFactory.createCheckbox());
```
