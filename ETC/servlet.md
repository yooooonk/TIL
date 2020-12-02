# Servlet
 
- 자바 웹 어플리케이션의 구성요소 중 동적인 처리를 하는 프로그램의 역할
- WAS에서 동작하는 JAVA 클래스
- HttpServlet 클래스를 상속받아야 함
- 서블릿과 JSP로부터 최상의 결과를 얻으려면, 웹 페이지를 개발할 때 이 두가지를 조화롭게 사용해함
    ex] 웹 페이지를 구성하는 화면(HTML)은 JSP로 표현하고, 복잡한 프로그래밍은 서블릿으로 구현
- Servlet 3.0 이상에서는 web.xml 파일을 사용하지 않고, java 어노테이션을 사용
- Servlet 3.0 미만에서는 servlet을 등록할 때 web.xml 파일에 등록
- 프레임워크를 사용하는 경우 프레임워크가 관리함

### Life Cycle
- servlet 객체의 생성부터 소멸까지의 과정
- HttpServlet의 3가지 메서드를 오버라이딩
    - init()
    - service(request, response) : 클라이언트의 요청이 GET일 경우 doGet(request,response) 메서드 호출, POST일 경우 doPost(request,response)를 호출
    - destroy()
- WAS는 서블릿 요청을 받으면 해당 서블릿이 메모리에 있는지 확인함
    - 메모리에 없으면 해당 서블릿 클래스를 메모리에 올리고 init() 메서드 실행
    - 메모리에 있으면 service() 메서드 실행
- WAS가 종료되거나 웹 어플리케이션이 새롭게 갱신될 경우 destroy() 메서드 실행

### Request, Response 객체
- 응답을 주고 받기 위해 사용하는 객체
- WAS는 웹 브라우저로부터 Servlet 요청을 받으면, 
    - 요청할 때 가지고 있는 정보를 HttpServletRequest 객체를 생성해 저장
    - 웹 브라우저에 응답을 보낼 때 사용하기 위해 HttpServletResponse 객체를 생성
    - 생성된 HttpServletRequest, HttpServletResponse 객체를 서블릿에게 전달
- HttpServletRequest
    - http 프로토콜의 request 정보를 서블릿에게 전달하기 위한 목적으로 사용
    - 헤더정보, 파라미터, 쿠키, URI, URL 등의 정보를 읽어 들이는 메서드를 가지고 있다
    - Body의 Stream을 읽어 들이는 메서드를 가지고 있다
- HttpServletResponse
    - 클라이언트에게 응답을 보내기 위한 객체
    - content type, 응답코드, 으답 메시지등을 전송
---
reference
- [edwith 부스트코스 웹프로그래밍 - servlet](https://www.edwith.org/boostcourse-web/lecture/16688/)