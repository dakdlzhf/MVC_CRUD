view/deleteForm.jsp
 
```jsp
<%@page import="com.mysql.cj.Session"%>
<%@ page contentType="text/html; charset=UTF-8"%>

<%
int memono = Integer.parseInt(request.getParameter("memono"));

%>
<!DOCTYPE html>
<html>
<head>
<title>homepage</title>
<meta charset="utf-8">
<style type="text/css">
#red {
	color: red;
}
</style>
</head>
<body>
	<div class="container">
		<h1 class="col-sm-offset-2 col-sm-10">삭제</h1>
		<form class="form-horizontal" action="deleteProc.do" method="post">
		
			<input type="hidden" name="memono" value="<%=memono%>" />
			
			
			<div class="form-group">
				<label class="control-label col-sm-2" for="passwd">비번</label>
				<div class="col-sm-6">
					<input type="password" name="passwd" id="passwd" class="form-control">
				</div>
			</div>

			<p id="red" class="col-sm-offset-2 col-sm-6">삭제하면 복구할수 없습니다.</p>


			<div class="form-group">
				<div class="col-sm-offset-2 col-sm-5">
					<button class="btn">삭제</button>
					<button type="reset" class="btn" onclick="history.back()">취소</button>
				</div>
			</div>
		</form>
	</div>
</body>
</html>

```

