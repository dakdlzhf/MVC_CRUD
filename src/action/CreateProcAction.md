src/action/CreateProcAction.java

```java
package action;

import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import model.MemoDAO;
import model.MemoDTO;

public class CreateProcAction implements Action {

	@Override
	public String execute(HttpServletRequest request, HttpServletResponse response) throws Throwable {
		
		MemoDAO dao = new MemoDAO();
		MemoDTO dto = new MemoDTO();
		
		dto.setWname(request.getParameter("wname"));
		dto.setTitle(request.getParameter("title"));
		dto.setContent(request.getParameter("content"));
		dto.setPasswd(request.getParameter("passwd"));
		
		boolean flag = dao.create(dto);
		
		request.setAttribute(null, response);
		return "/view/createProc.jsp";
	}

}

```



