# Notes

## Implementation Way One
``` Java
public interface Handler {
    boolean process(Request request);
}

public class AlphaHandler implements Handler {
    @Override
    public boolean process(Request request) {
        ...
    }
}

public class BetaHandler implements Handler {
    @Override
    public boolean process(Request request) {
        ...
    }
}

public class HandlerChain {
    private List<Handler> handlers = new ArrayList<>();

    public void addHandler(Handler handler) {
        handlers.add(handler);
    }

    public void process(Request request) {
        for (Handler handler : handlers) {
            if (handler.process(request)) {
                break;
            }
        }
    }
}
```

``` Java
HandlerChain chain = new HandlerChain();
chain.addHandler(new AlphaHandler());
chain.addHandler(new BetaHandler());

chain.process(request);
```

## Implementation Way Two
``` Java
public abstract class Handler {
    private Handler next;

    protected abstract boolean processNext(Request request);

    public boolean process(Request request) {
        if (processNext(request)) {
            return true;
        }
        if (next != null) {
            return next.process(request);
        }
        return false;
    }

    public void setNext(Handler handler) {
        next = handler;
    }
}

public class AlphaHandler extends Handler {
    @Override
    protected boolean processNext(Request request) {
        ...
    }
}

public class BetaHandler extends Handler {
    @Override
    protected boolean processNext(Request request) {
        ...
    }
}
```

``` Java
AlphaHandler alphaHandler = new AlphaHandler();
BetaHandler betaHandler = new BetaHandler();
alphaHandler.setNext(betaHandler);

alphaHandler.process(request);
```
