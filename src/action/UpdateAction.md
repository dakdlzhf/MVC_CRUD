

src/action/UpdateAction.java

```java
package action;

import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import model.MemoDAO;
import model.MemoDTO;

public class UpdateAction implements Action {

	@Override
	public String execute(HttpServletRequest request, HttpServletResponse response) throws Throwable {
		int memono = Integer.parseInt(request.getParameter("memono"));
		MemoDAO dao = new MemoDAO();
		MemoDTO dto = dao.read(memono);
		
		request.setAttribute("dto", dto);
		return "/view/updateForm.jsp";
	}

}

```

