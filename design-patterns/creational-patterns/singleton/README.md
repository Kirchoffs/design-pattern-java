# Notes
## Class Based Singleton
### Eager Initialization
```java
public final class Singleton {
    private static final Singleton instance = new Singleton();

    private Singleton() {
    }

    public static Singleton getInstance() {
        return instance;
    }
}
```

### Lazy Initialization
```java
public final class Singleton {
    private static Singleton instance = null;

    private Singleton() {
    }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

This way of creating a singleton is not thread-safe. If two threads call `getInstance` at the same time, they may both create a new instance of the singleton. This can be fixed by adding the `synchronized` keyword to the `getInstance` method. However, this can be inefficient as the synchronization is only needed the first time the singleton is created.

```java
public final class Singleton {
    private static Singleton instance = null;

    private Singleton() {
    }

    public synchronized static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

### Lazy Initialization with Double-Checked Locking (DCL)
```java
public final class Singleton {
    private static Singleton instance = null;

    private Singleton() {
    }

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

This also has a problem. The Java Memory Model allows the compiler to reorder instructions. This means that the `instance` variable can be assigned before the constructor is called. This can be fixed by declaring the `instance` variable as `volatile`.

```java
public final class Singleton {
    private static volatile Singleton instance = null;

    private Singleton() {
    }

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

## Enum Based Singleton
```java
public enum Singleton {
    INSTANCE;

    private String value;

    public void setValue(String value) {
        this.value = value;
    }

    public String getValue() {
        return value;
    }
}
```

```java
Singleton.INSTANCE.setValue("Hello, World!");
```
