



controller/Controller.java

```java
package controller;

import java.io.FileInputStream;
import java.io.IOException;
import java.util.Iterator;
import java.util.Map;
import java.util.Properties;

import action.Action;
import action.NullAction;
import jakarta.servlet.RequestDispatcher;
import jakarta.servlet.ServletConfig;
import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

public class Controller extends HttpServlet {
	private Map map = new java.util.HashMap();
	private boolean usingTemplate = false;
	private String templatePage = null;

	@Override
	public void init(ServletConfig config) throws ServletException {
		System.out.println("init 초기화");
		String configFile = config.getInitParameter("configFile");
		Properties properties = new Properties();
		FileInputStream fis = null;

		try {
			fis = new FileInputStream(configFile);
			properties.load(fis);
		} catch (IOException e) {
			e.printStackTrace();
		}
		Iterator keyIter = properties.keySet().iterator();

		while (keyIter.hasNext()) {
			String command = (String) keyIter.next();
			System.out.println("command : " + command);
			String handlerClass = properties.getProperty(command).trim();

			try {
				Class handler = Class.forName(handlerClass);
				Object actionClass = handler.newInstance();
				map.put(command, actionClass);
			} catch (Exception e) {
				e.printStackTrace();
			}
		}
		templatePage = config.getInitParameter("templatePage");

		if (templatePage != null && !templatePage.equals("")) {
			usingTemplate = true;
		}

	}

	@Override
	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		System.out.println("doGet 실행");
		process(request, response);
	}

	@Override
	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		System.out.println("doPost 실행");
		process(request, response);
	}

	private void process(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		String command = request.getRequestURI();
		System.out.println("브라우저요청 RequestURI : " + request.getRequestURI());

		if (command.indexOf(request.getContextPath()) == 0) {
			command = command.substring(request.getContextPath().length());
			System.out.println("브라우저요청 command : " + command);
		}

		Action action = (Action) map.get(command);

		if (action == null) {
			action = new NullAction();
		}

		String viewPage = null;
		try {
			viewPage = action.execute(request, response);

		} catch (Throwable e) {
			e.printStackTrace();
		}
		if (usingTemplate) {
			request.setAttribute("CONTENT_PAGE", viewPage);
			System.out.println("----------포워딩할 페이지---------");
			System.out.println("viewPage: " + viewPage);
		}

		RequestDispatcher dispatcher = request.getRequestDispatcher(usingTemplate ? templatePage : viewPage);
		dispatcher.forward(request, response);

	}

	@Override
	public void destroy() {
		System.out.println("destrory 소멸");

	}

}

```

