src/action/ReplyProcAction.java

```java
package action;

import java.util.HashMap;
import java.util.Map;

import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import model.MemoDAO;
import model.MemoDTO;

public class ReplyProcAction implements Action {

	@Override
	public String execute(HttpServletRequest request, HttpServletResponse response) throws Throwable {
		
	
		
		MemoDAO dao = new MemoDAO();
		MemoDTO dto = new MemoDTO();
		dto.setAnsnum(Integer.parseInt(request.getParameter("ansnum")));
		dto.setIndent(Integer.parseInt(request.getParameter("indent")));
		dto.setGrpno(Integer.parseInt(request.getParameter("grpno")));
		dto.setMemono(Integer.parseInt(request.getParameter("memono")));
		
		dto.setWname(request.getParameter("wname"));
		dto.setTitle(request.getParameter("title"));
		dto.setContent(request.getParameter("content"));
		dto.setPasswd(request.getParameter("passwd"));
		
		
		boolean flag = dao.createReply(dto);
			
		request.setAttribute("flag", flag);
		
		return "/view/replyProc.jsp";
		
	}

}

```

