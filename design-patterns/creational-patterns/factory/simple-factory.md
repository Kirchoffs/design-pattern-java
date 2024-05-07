# Notes
Product:
```
interface GUI {}

public class Button implements GUI {}

public class Checkbox implements GUI {}
```

Factory:
```
public enum GUIType {
    BUTTON, CHECKBOX
}

public class GUIFactory {
    public static GUI create(GUIType type) {
        switch (type) {
            case BUTTON:
                return new Button();
            case CHECKBOX:
                return new Checkbox();
            default:
                throw new IllegalArgumentException("Unknown type: " + type);
        }
    }
}
```

Usage:
```
List<GUI> guis = new ArrayList<>();
guis.add(GUIFactory.create(GUIType.BUTTON));
guis.add(GUIFactory.create(GUIType.CHECKBOX));
```
