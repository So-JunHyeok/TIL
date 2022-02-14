
## Annotation(@Component)

### @Component

 - 빈 설정파일이 아니라 클래스에서 빈을 직접등록 할 수 있도록 해주는 어노테이션 

### 사용법 

 - Component Scan에 @Component를 붙인 클래스를 스캔 할 수 있도록 설정해주어야 한다. 

### XML 설정 

 - base-package에 스캔 할 패키지를 설정한다.
 - 패키지가 여러개인 경우 <context:component-scan>를 여러개 설정한다.


```

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
	                    http://www.springframework.org/schema/beans/spring-beans.xsd
	                    http://www.springframework.org/schema/context
	                    http://www.springframework.org/schema/context/spring-context.xsd">
	                    
	<!-- 지정된 패키지 안에 있는 Bean 클래스들의 어노테이션을 분석하도록 지정한다 -->
	<context:component-scan base-package="com.atoz_develop.beans1"/>
	<context:component-scan base-package="com.atoz_develop.beans2"/>
</beans>

```

### @Configuration 설정 

 - @Configuration를 사용할 경우 @ComponentScan 어노테이션의 basePackages를 사용해서 패키지를 설정한다.
 - 패키지가 여러개일 경우 배열 지정 또는 @ComponentScan여러개를 사용한다.

```

@Configuration
// 지정된 패키지의 Bean 클래스들의 어노테이션을 분석하여 Bean을 등록하라고 지정한다.
@ComponentScan(basePackages = {"com.atoz_develop.beans", "com.atoz_develop.bean1"})
@ComponentScan(basePackages = "com.atoz_develop.beans2")
@ComponentScan(basePackages = "com.atoz_develop.beans3")

public class BeanConfigClass { }

```


### 참조 
Link:  [@Component 애노테이션 및 함께 사용하는 애노테이션 정리] (https://atoz-develop.tistory.com/entry/Spring-Component-%EC%95%A0%EB%85%B8%ED%85%8C%EC%9D%B4%EC%85%98-%EB%B0%8F-%ED%95%A8%EA%BB%98-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-%EC%95%A0%EB%85%B8%ED%85%8C%EC%9D%B4%EC%85%98-%EC%A0%95%EB%A6%AC)
