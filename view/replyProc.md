view/replyProc.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" %>
<%
	boolean flag= (boolean)request.getAttribute("flag");
%>


<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
<div class="container">
	<%   if(flag){
			out.println("답변 성공");
		}else{
			out.println("답변 실패.");
		}
	
	%>
	
	<button class='btn' onclick="location.href='create.do'">다시등록</button>
	<button class='btn' onclick="location.href='list.do'">목록</button>
	
	</div>
	

</body>
</html>
```

