# :pencil: TIL (2022.03.03)
## DAY 12
:book: 오늘 읽은 범위 : 7장. Error-Handling(오류 처리)
---
> :smile: **책에서 기억하고 싶은 내용을 써보세요.**
 - 오류 코드보다 예외를 사용하라(p.130)
 - Try-Catch-Finally 문부터 작성하라(p.132)
```
  어떤 면에서 try 블록은 트랜잭션과 비슷하다. 
  try 블록에서 무슨 일이 생기든지 catch 블록은 프로그램 상태를 일관성 있게 유지 해야 한다.
  그러므로 예외가 발생할 코드를 짤 때는 try-catch-finally 문으로 시작하는 편이 낫다.
```
 - 미확인(unchecked) 예외를 사용하라(p.133)
 - 예외에 의미를 제공하라(p.135)
 - 호출자를 고려해 예외 클래스를 정의하라(p.135)
```
감싸는(wrapper) 클래스는 매우 유용하다.
실제로 이부 API를 사용할 때는 감싸기 기법이 최선이다.
외부 API를 감싸면 외부 라이브러리와 프로그램 사이에서 의존성이 크게 줄어든다.
나중에 다른 라이브러리로 갈아타도 비용이 적다.
또한 감싸기 클래스에서 외부 API를 호출하는 대신 테스트코드를 넣어주는 방법으로 프로그램을 테스트하기도 쉬워진다.
```
 - 정상 흐름을 정의하라(p.137)
   * 특수 사례 패턴(SPECIAL CASE PATTERN) : 총액계산을 기존 class을 impletment 한 class에서 계산하여 가지고 있음.
 - null을 반환하지 마라(p.138)
   * null을 반환하니깐 NPE가 발생하지.
   * null list를 반환하려면 ```Collections.emptyList()```를 반환하자.
 - null을 전달하지 마라(p.140) 
   * null이 인수로 넘어오면 코드에 문제가 있다는 말이다.
 - 결론
```
오류 처리를 프로그램 논리와 분리해 독자적인 사안으로 고려하면 튼튼하고 깨끗한 코드를 작성할 수 있다.
오류 처리를 프로그램 논리와 분리하면 독립적인 추론이 가능해지며 코드 유지보수성도 크게 높아진다.
```
 
  
> :mag_right: **궁금한 내용이 있거나, 잘 이해되지 않는 내용이 있다면 적어보세요.**
 - JAVA Excepton
![](https://camo.githubusercontent.com/81791ce78fda8a42b3d72a2bcff7d1fa4b4a571df81292f53e26454340c42f31/68747470733a2f2f696d67312e6461756d63646e2e6e65742f7468756d622f523132383078302f3f73636f64653d6d746973746f72793226666e616d653d68747470733a2f2f626c6f672e6b616b616f63646e2e6e65742f646e2f526f5a6c562f6274715333493041586a4e2f61644d6f5937436556583859436666496c4e436f48302f696d672e706e67)
**Checked Exception**
- 컴파일러가 확인 할 수 있다. -> RuntimeException 외 전부
- 해당 경우 컴파일러가 exception처리 부분을 강제하는데, 미처리 시 컴파일 에러
- 주로 외부의 영향에 의해 발생

**Unchecked Exception**
- 컴파일러가 확인 불가 -> RuntimeException이하
- 프로그램 코드에 의한 에러.
- *호출하는 쪽에서 해당 메소드 호출 시 어떤 에러가 발생 가능한 지 반드시 체크 해야 함,*

*[unchecked Exception에 대한 오해](https://github.com/ByungJun25/study/tree/main/java/whiteship-study/9week)*
>`Springframework`에서는 `Transaction`설정과 관련하여 `Unchecked Exception`에 대해 `roll-back`기능을 지원합니다. 하지만 이는 `Springframework`의 `transaction`설정이 제공하는 것이지, 순수 자바 언어에서 지원하는 것이 아닙니다. 이 기능은 `springframework`가 구현한 기능일뿐, **`java`가 제공해주는  `Unchecked Exception`은  `roll-back`  기능이 없습니다.** 따라서 이를 `java`에서 제공해준다고 알고 있지 않기를 바랍니다.
- 트랜잭션 부분(rollback)은 spring 정책으로 변경 될 수 있으니 진리는 아니다.

- *from. 예전에 진행했던 [java study](https://github.com/myBabyGrand/study_JAVA_whiteship_live-study/blob/main/md_doc/09.Exception.md)에서 복습겸*

> :sunglasses: 소감 세줄 요약
 - *"try 블록은 트랜잭션과 비슷하다."* 이부분은 실제로 트랜잭션 처리를 위해 try블록을 자주 사용하는데 소름 비슷한게 돋았다. :scream:
 - *"먼저 강제로 예외를 일으키는 테스트 케이스를 작성한 후 테스트를 통과하게 코드를 작성하는 방법을 권장한다."*  오.. 꿀팁 :honey_pot: try 블록 내 트랜잭션의 순수성(?)을 유지할 수 있겠음 :thinking:
 - ```null```을 인수로 사용한 적이 몇몇 기억난다. 지금 생각해보면 interface나, abstract를 이용해서 구현할 수도 있었을 텐데 그땐 그게 최선이었나 보다. 아는 만큼 보인다는건 ```true```
 
 