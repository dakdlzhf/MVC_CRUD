view/read.jsp

```jsp
<%@page import="model.MemoDTO"%>
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>

<
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script>
	function update(memono){
		let url = 'update.do?memono='+memono;
		location.href = url;
	}
	function del(memono){
		let url = 'delete.do?memono='+memono;
		location.href = url;
	}
	function reply(memono){
		let url = 'reply.do?memono='+memono;
		location.href = url;
	}
</script>
</head>
<body>

<%
	int memono = Integer.parseInt(request.getParameter("memono"));
	MemoDTO dto = (MemoDTO)request.getAttribute("dto");
	
%>
	<div class="container">
		<h1 class="col-sm-offset-2 col-sm-10">메모</h1>
		<div class="panel panel-default">

			<div class="panel panel-default">
				<div class="panel-heading">이름</div>
				<div class="panel-body"><%=dto.getWname()%></div>

				<div class="panel-heading">제목</div>
				<div class="panel-body"><%=dto.getTitle()%></div>

				<div class="panel-heading">내용</div>
				<div class="panel-body"><%=dto.getContent()%></div>


				<div class="panel-heading">조회수</div>
				<div class="panel-body"><%=dto.getViewcnt()%></div>
				
				<div class="panel-heading">등록일</div>
				<div class="panel-body"><%=dto.getWdate()%></div>
				

			</div>
			<div>
			<button type="button" class="btn" onclick="location.href='create.do'">등록</button>
			<button type="button" class="btn" onclick="update('<%= memono %>')">수정</button>
			<button type="button" class="btn" onclick="del('<%= memono %>')">삭제</button>
			<button type="button" class="btn" onclick="reply('<%= memono %>')">답변</button>
			<button type="button" class="btn" onclick="location.href='list.do'">목록</button>
			</div>
		</div>
</body>
</html>
```
 
