view/deleteProc.jsp

```jsp
<%@ page import="java.util.*" %>
<%@ page import="utility.*" %>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" import="utility.*" %>
    
<% request.setCharacterEncoding("utf-8"); %> 
   
  
    
<%
	
	boolean pflag = (boolean)request.getAttribute("pflag");
	boolean flag = (boolean)request.getAttribute("flag");
%>




<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
<div class="container">
	<%  
		if(!pflag){
			out.print("잘못된 비밀번호 입니다");
		}else if(flag){
			out.println("삭제 성공");
		}else{
			out.println("삭제 실패.");
		}
	
	%>
	<% if(!pflag){ %>
		<button class='btn' onclick="history.back()">다시시도</button>
	<% } %>
	<button class='btn' onclick="location.href='create.do'">다시등록</button>
	<button class='btn' onclick="location.href='list.do'">목록</button>
	
	</div>
	

</body>
</html>
```

