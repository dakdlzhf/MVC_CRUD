src/action/Action.java ( Interface )

```java
package action;

import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

public interface Action {
	String execute(HttpServletRequest request,HttpServletResponse response) throws Throwable;
}

```

