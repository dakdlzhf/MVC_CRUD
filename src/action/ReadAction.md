src/action/ReadAction.java

```java
package action;

import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import model.MemoDAO;
import model.MemoDTO;

public class ReadAction implements Action {

	@Override
	public String execute(HttpServletRequest request, HttpServletResponse response) throws Throwable {
		
		int memono = Integer.parseInt(request.getParameter("memono"));
		
		MemoDAO dao =new MemoDAO();
		dao.upviewcnt(memono);
		MemoDTO dto = dao.read(memono);
		
		request.setAttribute("dto", dto);
		
		return "/view/read.jsp";
	}

}

```

