# Notes
__Interface Segregation Principle (ISP)__

## Cache Example
Original:
```java
public class Cache {
    public Object get(Object key) {}
    public void put(Object key, Object value) {}
    public void delete(Object key) {}
    public void rebuild(Config config) {}
}
```

Optimized:
```java
public interface Cache {
    Object get(Object key);
    void put(Object key, Object value);
    void delete(Object key);
}

public interface CacheManageable {
    void rebuild(Config config);
}

public class MyCache implements Cache, CacheManageable {
    @Override
    public Object get(Object key) {}

    @Override
    public void put(Object key, Object value) {}

    @Override
    public void delete(Object key) {}

    @Override
    public void reconfig(Config config) {}
}
```

## Model Example
Original:
```java
public class Modem {
    public void dial(String number) {};
    public void hangup() {};

    public void send(Data data) {};
    public Data recv() {};
}
```

Optimized:
```java
public interface Connection {
    void dial(String number);
    void hangup();
}

public interface DataChannel {
    void send(Data data);
    Data recv();
}

public class Modem implements Connection, DataChannel {
    @Override
    public void dial(String number) {}

    @Override
    public void hangup() {}

    @Override
    public void send(Data data) {}

    @Override
    public Data recv() {}
}
```

## Door Example
Original:
```java
public class Door {
    public void lock() {};
    public void unlock() {};
    public boolean isDoorOpen() {};
}

public interface TimerClient {
    void timeout();
}

public class Timer {
    public void register(int timeout, TimerClient client) {};
}
```

```java
public class Door implements TimerClient {
    public void lock() {};
    public void unlock() {};
    public boolean isDoorOpen() {};
    
    @Override
    public void timeout() {
      lock();
    }
}
```

Optimized using adapter:
```java
public class DoorTimerAdapter implements TimerClient {
    private Door door;

    @Override
    public void timeout() {
        door.lock();
    }
}
```

Optimized using interface segregation principle:
```java
public class TimedDoor extends Door implements TimerClient {
    @Override
    public void timeout() {
        lock();
    }
}
```
