

view/list.jsp

```jsp
<%@page import="model.MemoDTO"%>
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ page import="java.util.*, utility.*"%>

<%
String col = (String) request.getAttribute("col");
String word = (String) request.getAttribute("word");
String paging = (String) request.getAttribute("paging");
List<MemoDTO> list = (List<MemoDTO>) request.getAttribute("list");
int nowPage = (int) request.getAttribute("nowPage");
%>

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script>
	function read(memono) {
		let url = 'read.do?memono=' + memono;
		location.href = url;
	}
</script>
</head>
<body>
	<div class="container">
		<h1 class="col-sm-offset-2 col-sm-10">게시판 목록</h1>

		<form class="form-inline" action="list.do">
			<div class="form-group">
				<select class="form-control" name="col">
					<option value="wname" <%if (col.equals("wname"))
						out.print("selected");%>>이름</option>
					<option value="title" <%if (col.equals("title"))
						out.print("selected");%>>제목</option>
					<option value="content" <%if (col.equals("content"))
						out.print("selected");%>>내용</option>
					<option value="title_content" <%if (col.equals("title_content"))
						out.print("selected");%>>제목+내용</option>
					<option value="total" <%if (col.equals("total"))
						out.print("selected");%>>전체출력</option>
				</select>
			</div>
			<div class="form-group">
				<input type="text" class="form-control" placeholder="Enter 검색어" name="word" value="<%=word%>" />
			</div>
			<button class="btn btn-default">검색</button>
			<button class="btn btn-default" type="button" onclick="location.href='create.do'">등록</button>
		</form>
		<table class="table table-striped">
			<thead>
				<tr>
					<th>번호</th>
					<th>제목</th>
					<th>이름</th>
					<th>등록날짜</th>
					<th>grpno</th>
					<th>indent</th>
					<th>ansnum</th>
				</tr>
			</thead>
			<tbody>
				<%
				if (list.size() == 0) {
				%>
				<tr>
					<td colspan='7'>등록된 글이 없습니다.</td>
				</tr>

				<%
				} else {
				for (int i = 0; i < list.size(); i++) {
					MemoDTO dto = list.get(i);
				%>


				<tr>
					<td><%=dto.getMemono()%></td>
					<td>
						<%
						for (int j = 0; j < dto.getIndent(); j++) {
							out.print("&nbsp;&nbsp");
						}
						if (dto.getIndent() > 0) {
							out.print("<img src='../images/re.jpg'/>");
						}
						%> <a href="javascript:read( '<%=dto.getMemono()%>' )"><%=dto.getTitle()%></a>


					</td>
					<td><%=dto.getWname()%></td>
					<td><%=dto.getWdate()%></td>
					<td><%=dto.getGrpno()%></td>
					<td><%=dto.getIndent()%></td>
					<td><%=dto.getAnsnum()%></td>
				</tr>
				<%
				} //for end 
				} // if end
				%>
			</tbody>
		</table>
		<div>
			<%=paging%>
		</div>
	</div>
</body>
</html>
```

