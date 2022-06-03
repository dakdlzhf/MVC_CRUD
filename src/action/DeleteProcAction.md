src/action/DeleteProcAction.java

```java
package action;

import java.util.HashMap;
import java.util.Map;

import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import model.MemoDAO;

public class DeleteProcAction implements Action {

	@Override
	public String execute(HttpServletRequest request, HttpServletResponse response) throws Throwable {
		int memono = Integer.parseInt(request.getParameter("memono"));
		String passwd =request.getParameter("passwd");
		Map map = new HashMap();
		MemoDAO dao = new MemoDAO();
		
		map.put("memono",memono);
		map.put("passwd",passwd);
		boolean pflag = dao.passCheck(map);
		boolean flag = false;
		if(pflag){
			flag = dao.delete(memono);
		}
		
		
		
		
		request.setAttribute("flag", flag);
		request.setAttribute("pflag", pflag);
		
		return "/view/deleteProc.jsp";
	}

}

```

