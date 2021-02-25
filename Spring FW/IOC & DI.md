IOC와 DI
=================

Spring Container란 무엇인가?
------------------------
 Spring Framework에는 제공할 클래스들을 담고 관리하는 컨테이너가 존재한다.  
Spring F/W가 제공하는 클래스들이 담긴 컨테이너를 IOC 컨테이너 혹은 Spring 컨테이너라고 한다.  
스프링 컨테이너는 **서블릿**이다. Spring Framework 설치 시 WAS의 서블릿 컨테이너 내 스프링 컨테이너가 생성된다.  
스프링 컨테이너 내의 객체들을 bean이라고 한다. bean들은 HashMap 형태로 보관되어 있다. (Key:Value 형태)  
여기서 클래스가 아닌 객채라고 표현한 이유는 Container는 제공할 클래스를 new해서 object 형태로 보관하고 있다.  
스프링 컨테이너는 이 bean의 생성, 소멸 등 라이프 사이클 관리를 한다.  
가장 중요한 기능으로는 개발자가 특정 bean에 대한 사용 요청을 할 시 이를 제공해주는 역할을 한다.

IOC란 무엇인가?
---------------
 여기서 잠깐, 기존에 우리는 사용하고 싶은 클래스가 있을 시 코드에 직접 해당 클래스를 new하여 사용했다.  
그러나 Spring FrameWork 기반에서는 개발자가 new를 하는 것이 아닌 Spring Container가 new를 하고 개발자는 이를 요청하여 사용한다.  
즉, 객체에 대한 제어(생성, 소멸 등)권한이 개발자에 있는 것이 아닌 스프링 컨테이너에게 있다.  
이를 **제어의 역전**(Inversion of Controll)이라고 한다.  
제어 역전은 Spring FrameWork의 가장 중요한 기능 중 하나이다.   
여기서 들 수 있는 의문점은 스프링 컨테이너 내 내가 사용하고 싶은 object가 없으면 어떡하냐는 것이다.  
이를 위해 개발자는 사용할 bean을 직접 스프링 컨테이너에 등록할 수 있다.

DI란 무엇인가?
---------------
의존성 주입(Dependency Injection, DI)은 프로그래밍에서 구성요소간의 의존 관계가 소스코드 내부가 아닌 외부의 설정파일 등을 통해 정의되게 하는 디자인 패턴 중의 하나이다.  
의존성에 대한 말을 먼저 해보면, 간단하게 A 클래스 내에서 B 클래스의 메소드를 사용하고 싶을 경우 B 객체를 만들어 사용한다.  
이 때, B 클래스 메소드(A가 사용 중인)를 수정하면, A 클래스에서도 수정한 내용이 반영된다. 즉, A 클래스가 B 클래스를 의존한다.  
이를 다른 표현으로 A가 B에 강하게 결합한다고도 하는데, 이럴 경우 발생하는 문제점이 무엇인지 예제로 살펴보자.  

```java
// A 클래스
Class A() {
  String animal = "고양이"
  B b = new B();
  b.voice(animal);
}

// B 클래스
Class B() {
  public void voice(String animal){
    System.out.println(animal + "는 야옹");
  }
}
```
B 클래스는 고양이의 울음소리를 출력해주는 메소드인 voice를 가지고 있었다. 따라서 고양이 변수를 가진 A는 울음소리를 듣기위해 B 클래스의 voice를 사용하고 있었다.

**B 클래스 변경**

```java
Class B() {
  public void voice(String animal){
    System.out.println(animal + "은 멍멍");
  }
}
```

그런데, 이제는 고양이 보단 강아지가 좋아 고양이 울음소리가 아닌 강아지 울음소리를 내도록 voice 메소드를 변경했다.  
고양이가 멍멍할 수는 없으니 A 클래스의 animal 변수도 강아지로 변경 해주었다.  

**B 클래스 변경에 의한 A 클래스 변경(의존)**

```java
// A 클래스
Class A() {
  String animal = "강아지"
  B b = new B();
  b.voice(animal);
}
```

여기 까진 괜찮다. 그런데 기존 B 클래스의 메소드를 사용하고 있던 클래스가 100개, 1000개라면? 어쩔 수 없이 개발자가 수동으로   
각 클래스의 animal을 고양이 => 강아지로 일일히 변경해주어야 하는 매우 귀찮은 일이 발생한다.  

DI를 이용하면 이러한 문제를 해결할 수 있다. 
DI 방식을 사용하면 한 클래스 내 다른 객체를 사용할 시, 해당 클래스에 객체를 직접 new 하지 않는다.  
대신 사용할 객체를 스프링 컨테이너의 bean으로 등록 해놓고 이를 받아서 사용한다.  
Bean으로 등록된 클래스는 스프링 컨테이너가 자동으로 new를 하여 객체 형태로 보관하고 있기 때문에
어느 클래스이건 해당 객체를 사용하고 싶으면 getBean()이라는 메소드를 사용하여 받아서 사용하면 된다.  
즉, 스프링 컨테이너가 객체를 '주입'시켜 줌으로써 객체간 직접적인 의존관계가 발생하지 않는다.
예제 코드를 보자.

**DI를 사용한 객체 주입**

```
// B.java
package di_example2;

Class B() {
  Private String animal;
  Private String animalVoice;
  
  public B(String animal, String animalVoice){
    this.animal = animal;
    this.animalVoice = animalVoice;
  }
  
  public void voice(){
    System.out.println(animal + "은" + animalVoice);
  }
}

// A.java

package di_example2;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.GenericXmlApplicationContext;

Class A() {
  //application.xml 파일 내 B 빈을 가져오기 위한 코드
  ApplicationContext ctx = new GenericXmlApplicationContext("application.xml");
  B b = ctx.getBean("b", B.class);
  b.voice();


}

// application.xml

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

<bean id="B" class="di_example.B">
<constructor-arg value="강아지 " /> 
<constructor-arg> <value> 멍멍</value> </constructor-arg> 

</bean>
</beans>

```
동물이나 울음소리를 바꿔야 할 경우 이제는 코드를 직접 수정하는 것이 아니라, 등록된 bean의 설정만 바꾸어주면 된다.
이렇게 되면 해당 bean을 get하고 있는 다른 클래스에 이 변경사항이 자동으로 적용된다.

결론
-------
IOC, DI 방식을 사용하여 얻게되는 이점을 말해보자면 유지보수가 용이해진다는 것이다.  
코드의 변경 사항이 있을 경우 이를 일일히 바꾸는 것이 아니라 bean 설정만 수정 해주면 되기 때문이다.
