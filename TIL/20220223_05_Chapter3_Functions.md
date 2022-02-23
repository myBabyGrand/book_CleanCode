
# :pencil: TIL (2022.02.23)
## DAY 5,6
:book: 오늘 읽은 범위 : 3장. Functions(함수)
---

> :smile: **책에서 기억하고 싶은 내용을 써보세요.**
> 

 - 작게 만들어라!(p.42)
 - 한 가지만 해라!(p.44)
 - 함수 당 추상화 수준은 하나로!(p.45) 
    * 위에서 아래로 코드 읽기 : 내려가기 규칙
    * 코드는 위에서 아래로 이야기처럼 읽혀야 좋다.
 - Switch 문(p.47)
    * switch문은 작게 만들기 어렵다.(if/else의 연속도 마찬가지)
    * 다형성을 이용하여 switch문을 abstract factory에 숨겨 다형적 객체를 생성하는 코드 안에서만 switch를 사용하도록 한다.
 - 서술적인 이름을 사용하라!(p.49)
 - 함수 인수(p.50)
    * 함수에서 이상적인 인수 개수는 0개(무항)다.
    * 많이 쓰는 단항 형식
      + 인수 1개를 넘기는 경우 : 질의 ```boolean fileExists("MyFile") ```
      + 인수 1개를 넘기는 경우 : 변환 ```StringBuffer transform(StringBuffer in) ```
      + 이벤트 함수 : 이벤트임이 명확하게 들어나야 한다.
    * 플래그 인수 : 되도록이면 쓰지 말라
    * 이항 함수 : Point 클래스(2차원 좌표계)와 같은 경우만 적절
      + 단항으로 찢을 수 있다면 찢는다.
    * 삼항 함수 : 이항 함수와 같은 원리
    * 인수 객체
    ```JAVA
    Circle makeCircle(double x, double y, double radius);
    Circle makeCircle(Point center, double radius);//Point를 하나의 개념으로
    ```
    * 인수 목록 : ```String.format```과 같이 가변 인수를 취급할 경우
    * 동사와 키워드
      + 단항 함수는 동사-목적어 구조로: ```write(name)```, ```writeField(name)```
      + 함수에 키워드를 추가하여 기억하기 쉽도록 : ```assertExpectedEqualsActual(expect, actual)```
 - 부수 효과를 일으키지 마라!(p.54)
    * 1함수 1기능 원칙에 위배
    * 시간적 결합(temporal coupling)과 순서 종속성(order dependency)를 초래
    * 시간적 결합이 필요하다면 함수명에 명시하는 옳다.
    * 출력 인수 : 일반적으로 출력 인수는 피해야 한다. 함수에서 상태를 변경해야 한다면 함수가 속한 객체 상태를 변경하는 호출 방식이 좋다.
    ```JAVA
    public void appendFooter(StringBuffer report){
      ...
    }

    public class Report{
      ...
      
      public void appendFooter(){
        ...
      }
    }
    ```
 - 명령과 조회를 분리하라!(p.56)
    * 함수는 뭔가를 수행하거나, 뭔가에 답하거나 둘 중 하나만 해야 한다. 둘 다 하면 안된다.
 - 오류 코드보다 예외를 사용하라!(p.57)
    * Try/Catch 블록 뽑아내기
    ```JAVA
    try{
      deletePage(page);
      registry.deleteReference(page.name); 
      configKeys.deleteKey(page.name.makeKey());
   } catch(xception e) { 
      logger.log(e.getMessage());
   }

    //Try/Catch 블록 뽑아내기
    public void delete(Page page) {
      try {
         deletePageAndAllReferences(page);
      } catch (Exception e) {
         logError(e);
      }
   }   
   private void deletePageAndAllReferences(Page page) throws Exception { 
      deletePage(page);
      registry.deleteReference(page.name); 
      configKeys.deleteKey(page.name.makeKey());
   }
   private void logError(Exception e) { 
      logger.log(e.getMessage());
   }
    ```
   * 오류처리도 한가지 작업이다.
   * Error.java 의존성 자석(magnet)
      + 오류코드를 관리하는 class에 의존적, 새로운 오류코드가 추가되면 재컴파일/재배치 필요
      + 예외는 Exception class에서 파생, 재컴파일/재배치 없이도 새 예외 class 추가 가능
 - 반복하지 마라!
   * 코드의 중복이 많다면 요구사항이 변하면 고쳐야 할 곳도 많다.
   * 중복은 S/W영역에서는 만악의 근원

```
소프트웨어를 짜는 행위는 여느 글짓기와 비슷하다.
...
처음에는 길고 복잡하다. 들여쓰기 단계도 많고 중복된 루프도 많다.
...
그런 다음 나는 코드를 다듬고, 함수를 만들고, 이름을 바꾸고, 중복을 제거한다.
...
최종적으로 이 장에서 설명한 규칙을 따르는 함수가 얻어진다.
```
>*처음부터 탁 짜내지 않는다. 그게 가능한 사람은 없으리라*
  
> :mag_right: **궁금한 내용이 있거나, 잘 이해되지 않는 내용이 있다면 적어보세요.**
 - SOLID (출처 : [https://ko.wikipedia.org/wiki/SOLID_(객체_지향_설계)](https://ko.wikipedia.org/wiki/SOLID_(%EA%B0%9D%EC%B2%B4_%EC%A7%80%ED%96%A5_%EC%84%A4%EA%B3%84))
 
 두문자|	약어|	개념|
 ---|---|---
**S**	|SRP|	단일 책임 원칙 (Single responsibility principle)한 클래스는 하나의 책임만 가져야 한다.
**O**	|OCP|	개방-폐쇄 원칙 (Open/closed principle)“소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.”
**L**	|LSP|리스코프 치환 원칙 (Liskov substitution principle)“프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다.” 계약에 의한 설계를 참고하라.
**I**	|ISP|인터페이스 분리 원칙 (Interface segregation principle)“특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다.”
**D**	|DIP|	의존관계 역전 원칙 (Dependency inversion principle)프로그래머는 “추상화에 의존해야지, 구체화에 의존하면 안된다.” 의존성 주입은 이 원칙을 따르는 방법 중 하나다.

> :sunglasses: 소감 세줄 요약
 - *처음부터 탁 짜내지 않는다. 그게 가능한 사람은 없으리라*  :pray:
 - 첫 술에 배부르랴
 - 천리 길도 한걸음부터 :runner:
 
 