# enum

## 열거형[enum]이란?
 - 서로 관련된 상수들을 묶어 놓은것 
 - enum은 클래스이고 객체이다 따라서 메소드를 사용할 수 있다.

## enum의 사용법
  ### 데이터들의 연관관계를 표현
  - 다른 값 같은 의미를 가지는 값을 묶어서 표현 할 수 있기때문에 반복코드를 줄이고 값들의 의미를 알게 쉽게 할 수 있다.
  
  
 - enum클래스안에 상수를 타입으로 선언해서 사용 할 수 있다. 
```
 class Card {
  enum Kind{CLOVER, HEART, DIAMOND, SPADE}
  //enum Kind{CLOVER("0"), HEART("1"), DIAMOND("2"), SPADE("3")} // 타입의 값을 지정 할 수도 있다.
  enum Value{TWO, THREE, FOUR}
 }

```

 - 선언된 상수안에 같은 의미를 가지는 다른 형태의 값들을 모아두고 사용 할 수 있다.<br>
 -> Y라는 상태값을 서로 다르게 표현된 경우 모두 Y라는 상태값을 나타내는 값이라는 것을 쉽게 알 수 있음
 
```
  enum State{
    Y("1", true, 1), 
    N("0", false, 0)
    
    private String stateValue1;
    private boolean stateValue2;
    private int stateValue3;
    
   TableStatus(String s, boolean b, int c) {
      this.stateValue1 = s;
      this.stateValue2 = b;
      this.stateValue3 = c;
    }    
    
   public String getStateValue1(){
    return stateValue1;
   }
    
   public boolean getStateValue2(){
    return stateValue2;
   }
   
   public int getStateValue3(){
    return stateValue3;
   }   
    
  }
```
 - ex) 만약에 Y라는 값을 구조가 다른 각 테이블에 저장하고자 한다면 enum을 통해서 불필요한 코드를 줄이고 값들의 의미를 명확하게 확인 할 수 있다.
 
 ```
 
     public static void main(String[] args) {

        String state = "Y";

        TableStatus status = TableStatus.valueOf("Y"); // enum클래스에서 제공하는 메소드로 일치하는 상수값을 찾아준다.
        System.out.println("테이블1에 저장[String] : "+status.getStateValue1());
        System.out.println("테이블2에 저장[boolean] : "+status.getStateValue2());
        System.out.println("테이블3에 저장[int] : "+status.getStateValue3());

        
        테이블1에 저장[String] : 1
        테이블2에 저장[boolean] : true
        테이블3에 저장[int] : 0
       
    }
 
 ```
 
  ### 상태와 행위를 한곳에서 처리가능하다.
  - enum 타입의 클래스에 익명함수, 1급함수, 함수형 인터페이스를 활용한다면 상태와 행위를 한곳에서 처리할 수 있다.
 ```
 
public enum CalculatorType {

    // Function 함수형 인터페이스는 인자값을 받아서 인자값을 반환 할 수 있다.
    // 익명함수는 함수형 인터페이스를 통해서 접근할 수 있다.
    // 익명함수는 1급함수이기 때문에 변수에 함수를 할당 할 수 있다.
    // 생성자를 통해서 Funtion 인터페이를 인자로 받기 때문에 상수의 값에 익명함수를 사용 할 수 있다.
    CALC_A(value -> value),
    CALC_B(value -> value * 10),
    CALC_C(value -> value * 3),
    CALC_ETC(value -> 0L);

    private Function<Long, Long> expression;

    CalculatorType(Function<Long, Long> expression){
        this.expression = expression;
    }

    public long calculate(long value){ return expression.apply(value);}

} 
 public class Main {
    public static void main(String[] args) {

        CalculatorType code = CalculatorType.CALC_A;
        CalculatorType code2 = CalculatorType.CALC_B;
        CalculatorType code3 = CalculatorType.valueOf("CALC_C");

        System.out.println("code : "+code.calculate(5));
        System.out.println("code2 : "+code2.calculate(5));
        System.out.println("code3 : "+code3.calculate(5));

    }
    // 결과값 : 
    //code : 5
    //code2 : 50
    //code3 : 15
} 
 
 ```
 ### 데이터 그룹관리
  - 어떤 결제수단으로 진행되었는지, 해당 결제 방식이 어느 결제 종류에 속하는지 확인 할 수 있어야하는 조건이라면 
  - enum을 적용하지 않고 if문으로 구현한다면 

 ```
     public static String getPayGroup(String payCode){

       if("ACCOUNT".equals(payCode) || "REMITTANCE".equals(payCode) || "ON_SITE_PAYMENT".equals(payCode) || "TOSS".equals(payCode)){
            return "CASH";
        }else if("PAYCO".equals(payCode) || "CARD".equals(payCode) || "KAKAO_PAY".equals(payCode) || "BAEMIN_PAY".equals(payCode)){
            return "CARD";
        }else if("POINT".equals(payCode) || "COUPON".equals(payCode)){
            return "ETC";
        }else{
            return "EMPTY";
        }
    }
 ```
 - 위에 코드에서는 조건값과 리턴값의 관계[대체값? 포함관계?]를 확인 할 수 없다(실제로는 결제종류가 결제수단을 포함하고 있다)
 - 입력값과 결과값이 예측이 불가하기 때문에 결과값 추가시 그것을 검증하는 코드를 추가해야한다.
```
    public void pushByPayGroup(final String payGroupCode){
        if("CASH".equals(payGroupCode)){
            pushMethod(payGroupCode);
        }else if("CARD".equals(payGroupCode)){
            pushMethod(payGroupCode);
        }else if("ETC".equals(payGroupCode)){
            pushMethod(payGroupCode);
        }else{
            throw new RuntimeException("코드가 없습니다.");
        }
    }

    public void printByPayGroup(final String payGroupCode){
        if("CASH".equals(payGroupCode)){
            printMethod(payGroupCode);
        }else if("CARD".equals(payGroupCode)){
            printMethod(payGroupCode);
        }else if("ETC".equals(payGroupCode)){
            printMethod(payGroupCode);
        }else{
            throw new RuntimeException("코드가 없습니다.");
        }
    }
    public void pushMethod(String payGroupCode){
        System.out.println(payGroupCode+"결제push메소드 실행");
    }
    public void printMethod(String payGroupCode){
        System.out.println(payGroupCode+"결제print메소드 실행");
    }
```
 - 그룹별 기능을 추가하게 된다면 그룹을 나누는 코드를 계속 만들어야한다.


 
## 그 외 enum의 장점 
 
 - 상수를 사용시 대입하는 변수가 열거형이 아니면 의도치 않게 들어간 값의 유효성을 체크 할 수 없지만 enum타입으로 선언하면 선언된 상수만 할당이 가능하다.
 ```
 int KindValue = 5;
 int KindValue = Kind.CLOVER;
 
 Kind KindValue = 5; // 할당 할 수 없음;
 Kind KindValue = Kind.CLOVER;
 
 ```
 - Y라는 
 





















https://techblog.woowahan.com/2527/
