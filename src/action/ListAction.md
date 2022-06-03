src/action/ListAction.java

```java
package action;

import java.util.HashMap;
import java.util.List;
import java.util.Map;

import org.apache.tomcat.jakartaee.bcel.classfile.Utility;

import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import model.MemoDAO;
import model.MemoDTO;

public class ListAction implements Action {

	@Override
	public String execute(HttpServletRequest request, HttpServletResponse response) throws Throwable {
		// 1.model 사용 ,2.request 에 저장 , 3.view 선택 리턴

		// 검색관련---
		String col = model.Utility.checkNull(request.getParameter("col"));
		String word = model.Utility.checkNull(request.getParameter("word"));

		if (col.equals("total")) {
			word = "";
		}
		// 페이징 관련---
		int nowPage = 1;
		if (request.getParameter("nowPage") != null) {
			nowPage = Integer.parseInt(request.getParameter("nowPage"));
		}

		int recordPerPage = 5;

		int sno = ((nowPage - 1) * recordPerPage);
		int eno = recordPerPage;

		Map map = new HashMap();
		map.put("col", col);
		map.put("word", word);
		map.put("sno", sno);
		map.put("eno", eno);

		MemoDAO dao = new MemoDAO();

		List<MemoDTO> list = dao.list(map);
		int total = dao.total(map);
		String paging = model.Utility.paging(total, nowPage, recordPerPage, col, word);

		request.setAttribute("list", list);
		request.setAttribute("total", total);
		request.setAttribute("col", col);
		request.setAttribute("word", word);
		request.setAttribute("paging", paging);
		request.setAttribute("nowPage", nowPage);

		return "/view/list.jsp";
	}

}

```

