---
title: (WIP) JSP란
date: 2023-01-03 21:21:19
category: til
thumbnail: { thumbnailSrc }
draft: false
---

## **주의사항**

문서 정리에 획일화된 일관성이 없다.  
좋은 블로깅을 참고하고 나만의 획일화된 기술 문서 정리방법을 적립하자.  
그리고 글을 올리자. (출처는 명확히 표시하자.)  
예를 들어서 제목(#), 목차(##), tdlt??, 이런 것들...

## JSP란

JSP(JavaServer Pages)

> Java 언어를 기반으로 하는 `Server Side 스크립트 언어`  
> HTML 코드에 Java 코드를 넣어 동적인 웹 페이지를 생성하는 웹 애플리케이션 도구

### 나오게된 배경

원래 개발자가 정보를 사용자에게 보여주고 싶은 경우에  
웹 서버에서 index.html을 사람이 업데이트를 해야하는 공수가 필요했다.

그래서 이러한 문제를 해결하기 위해서
**CGI(Common Gateway Interface)**가 등장했다.

### CGI

클라이언트에서 정보 요청시 `프로세스`를 데이터 베이스 와 사용자 사이에 넣어서 클라이언트가 원하는 정보를 전달했다.
이렇게 동적 웹 프로그래밍 방식은 프로세스 방식으로 실행된다.

CGI 방식의 단점은 클라이언트의 요청이 있을 때마다 독립적인 프로세스를 생성한다는 것이다.  
이는 요청이 많아질수록 프로세스가 많아져 시스템에 부하를 주게 된다.  
[CGI 기술의 등장 배경과 WAS로의 발전](https://bentist.tistory.com/40)

#### 여기서 나온 기능이 JSP이다.

1.JSP로 Thred 기능을 써서 클라이언트가 요구하는 메모리를 최초 한 번만 로드하여서 다른 사용자가 같은 메모리를 원한다면 Thred가 재사용되어 Response(응답) 해준다.

2.JSP를 통해 정적인 HTML과 동적으로 생성된 contents(HTTP 요청 파라미터)를 혼합하여 사용할 수 있다. 즉, 사용자가 입력한 contents에 맞게 동적인 웹 페이지를 생성한다.

3.JSP 가 실행되면 자바 서블릿으로 변환되며 웹 애플리케이션 서버에서 동작되면서 필요한 기능을 수행하고 그렇게 생성된 데이터를 웹페이지와 함께 클라이언트로 응답합니다.

### 자바 서블릿(Java Servlet)

서블릿이란 웹페이지를 동적으로 생성하기 위해 서버측 프로그램을 말한다.
이는 자바 언어를 기반으로 만들지며 웹 어플리케이션 서버 ( Web Application Sever ) 위에서 컴파일 되고 동작한다.

jsp도 서블릿(servlet)?

### JSP 와 서블릿

JSP 와 서블릿의 차이점은 결과적으로 하는일은 동일하지만

JSP 는 HTML 내부에 JAVA 소스코드가 들어감으로 인해 HTML 코드를 작성하기 간편하다는 장점이있으며

서블릿은 자바코드내에 HTML 코드가 있어서 읽고 쓰기가 굉장히 불편하기 때문에 작업의 효율성이 떨어진다.

그래서 우리가 작성한 JSP가 서버로 요청될때 서블릿파일로 변환되어 JSP태그를 분해하고 추출해서 다시 순수한 HTML를 반환한다.

### 동작과정

1. 클라이언트가 어떤 동작을 함으로써 hello.jsp 를 요청하였다.

2. JSP 컨테이너가 JSP 파일을 읽는다.

3. JSP 컨테이너가 Generete (변환) 작업을 통해 Servlet ( .java ) 파일을 생성한다.

4. .java 파일은 다시 .class 파일로 컴파일된다.

5. Execute (실행) 을통해 HTML 파일을 생성하여 JSP 컨테이너 에게 전달한다.

6. JSP 는 HTTP 프로토콜을 통해 HTML 페이지를 클라이언트 에게 전달한다.

### JSP는

JSP 는스크립트 언어이기 때문에 자바 기능을 그대로 사용할 수 있다.

Tomcat(WAS)이 이미 만들어놓은 객체(predefined values)를 사용한다.

Ex. request, response, session 등

사용자 정의 태그(custom tags)를 사용하여, 보다 효율적으로 웹 사이트를 구성할 수 있다.

JSTL(JSP Standard Tag Library, JSP 표준 태그 라이브러리)사용

HTML 코드 안에 Java 코드가 있기 때문에 HTML 코드를 작성하기 쉽다.

Servlet과 다르게 JSP는 수정된 경우 재배포할 필요 없이 Tomcat(WAS)이 알아서 처리해준다.

### JSTL

- JSP Standard Tag Library, JSP 표준 태그 라이브러리
- 커스텀 태그 추가 기능 제공

### 강의(정리예정)

[JSP 웹 쇼핑몰 프로그래밍 기본 과정(JSP WEB Programming)](https://www.inflearn.com/course/jsp-%EC%9B%B9%EA%B0%9C%EB%B0%9C-%EC%87%BC%ED%95%91%EB%AA%B0-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/dashboard)  
[JSP WEB MVC Model2 Programming(중급 과정)](https://www.inflearn.com/course/jsp-%EC%9B%B9%EA%B0%9C%EB%B0%9C-mvc-model2-%EC%A4%91%EA%B8%89/dashboard)
