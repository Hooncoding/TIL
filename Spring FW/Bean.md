Bean 등록 및 getBean() 이용
===========================
Bean을 주입받아 사용하려면 먼저 Bean을 등록해야 한다.    
Bean은 스프링 컨테이너의 설정 파일인 xml 파일을 통해 설정할 수 있다.  

```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.1.xsd">

<!-- Bean 등록하기 -->

<bean id = "calc" class = "com.dylan.edu.di.Calculator"></bean>
<!-- 위 코드는 Calculator cals = new Calculator() 해서 컨테이너에 보관하라는 명령과 같다 -->

<bean id = "myCalc" class = "com.dylan.edu.di.MyCalc">
  <property name = "calc">
    <ref bean="calc"/>

```
