view/updateForm.jsp

```jsp
<%@page import="model.MemoDTO"%>
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>


<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<%
	MemoDTO dto = (MemoDTO)request.getAttribute("dto");
%>


<body>
	<div class="container">
	<h1> 게시판 수정</h1>
		<form class="form-horizontal" action="updateProc.do" method="post">

			<input type="hidden" name="memono" value="<%= dto.getMemono() %>"/>
	
			<div class="form-group">
				<label class="control-label col-sm-2" for="wname">작성자</label>
				<div class="col-sm-6">
					<input type="text" name="wname" id="wname" class="form-control" value="<%= dto.getWname() %>">
				</div>
			</div>

			<div class="form-group">
				<label class="control-label col-sm-2" for="title">제목</label>
				<div class="col-sm-6">
					<input type="text" name="title" id="title" class="form-control" value="<%= dto.getTitle() %>">
				</div>
			</div>


			<div class="form-group">
				<label class="control-label col-sm-2" for="content">내용</label>
				<div class="col-sm-6">
					<input type="text" name="content" id="content" class="form-control" value="<%= dto.getContent() %>">
				</div>
			</div>

			<div class="form-group">
				<label class="control-label col-sm-2" for="passwd">패스워드</label>
				<div class="col-sm-6">
					<textarea rows="5" cols="5" id="passwd" name="passwd" class="form-control"></textarea>
				</div>
			</div>

			<div class="form-group">
				<div class="col-sm-offset-2 col-sm-5">
					<button class="btn">수정</button>
					<button type="reset" class="btn" onclick="history.back()">취소</button>
				</div>
			</div>
		</form>
	</div>
</body>
</html>
```

