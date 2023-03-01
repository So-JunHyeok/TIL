# enum

## 열거형[enum]이란?
 - 서로 관련된 상수들을 묶어 놓은것 
 - enum은 클래스이고 객체이다 따라서 메소드를 사용할 수 있다.

## enum의 사용법
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
 
## enum의 장점 
 
 - 상수를 사용시 대입하는 변수가 열거형이 아니면 의도치 않게 들어간 값의 유효성을 체크 할 수 없지만 enum타입으로 선언하면 선언된 상수만 할당이 가능하다.
 ```
 int KindValue = 5;
 int KindValue = Kind.CLOVER;
 
 Kind KindValue = 5; // 할당 할 수 없음;
 Kind KindValue = Kind.CLOVER;
 
 ```
 - Y라는 
 
