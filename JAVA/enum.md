# enum

## 열거형[enum]이란?
 - 서로 관련된 상수들을 묶어 놓은것 
 - enum은 클래스이고 객체이다 따라서 메소드를 사용할 수 있다.
```
 class Card {
  enum Kind{CLOVER, HEART, DIAMOND, SPADE}
  enum Value{TWO, THREE, FOUR}
 }
 
```
## enum의 장점 
 
 - 상수를 사용할떄 대입하는 변수가 열거형이 아니면 의도치 않게 들어간 값의 유효성을 체크 할 수 없지만 enum타입으로 선언하면 선언된 상수만 할당이 가능하다.
 ```
 int KindValue = 5;
 int KindValue = Kind.CLOVER;
 
 Kind KindValue = 5; // 할당 할 수 없음;
 Kind KindValue = Kind.CLOVER;
 
 ```

 
