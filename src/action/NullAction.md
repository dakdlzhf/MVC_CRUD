src/action/NullAction.java

```java
package action;

import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

public class NullAction implements Action {

	@Override
	public String execute(HttpServletRequest request, HttpServletResponse response) throws Throwable {
		
		return "/view/nullCommand.jsp";
	}

}

```

