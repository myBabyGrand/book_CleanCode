
# :pencil: TIL (2022.02.24~2022.02.25)
## DAY 7,8
:book: 오늘 읽은 범위 : 4장. Comments(주석)
---

> :smile: **책에서 기억하고 싶은 내용을 써보세요.**
> 
```나쁜 코드에 주석을 달지 마라, 새로 짜라.```
 - 주석은 나쁜 코드를 보완하지 못한다(p.69)
 - 코드로 의도를 표현하라(p.70)
 - 좋은 주석(p.70)
   * 법적인 주석
   * 정보를 제공하는 주석
   * 의미를 설명하는 주석
   ```JAVA
   // 스레드를 대량 생성하는 방법으로 어떻게든 경쟁 조건을 만들려 시도한다. 
   for (int i = 0; i > 2500; i++) {
      WidgetBuilderThread widgetBuilderThread = 
         new WidgetBuilderThread(widgetBuilder, text, parent, failFlag);
      Thread thread = new Thread(widgetBuilderThread);
      thread.start();
   }
   ```
   * 의미를 명료하게 밝히는 주석
   ```JAVA
   // 여유 시간이 충분하지 않다면 실행하지 마십시오.
   public void _testWithReallyBigFile() {
   ```
   * 결과를 경고하는 주석
   * TODO 주석
   * 중요성을 강조하는 주석
   ```JAVA
   String listItemContent = match.group(3).trim();
   // 여기서 trim은 정말 중요하다. trim 함수는 문자열에서 시작 공백을 제거한다.
   // 문자열에 시작 공백이 있으면 다른 문자열로 인식되기 때문이다. 
   ```
   * 공개 API에서 Javadocs
 - 나쁜 주석(p.75)
   * 주절거리는 주석
   * 같은 이야기를 중복하는 주석
   * 오해할 여지가 있는 주석
   * 의무적으로 다는 주석
   * 이력을 기록하는 주석
   * 있으나 마나 한 주석
   * 무서운 잡음
   * 함수나 변수로 표현할 수 있다면 주석을 달지 마라
   * 위치를 표시하는 주석
   * 닫는 괄호에 다는 주석
   * 공로를 돌리거나 저자를 표시하는 주석
   * 주석으로 처리한 코드
   * HTML주석
   * 전역 정보
   * 너무 많은 정보
   * 모호한 관계
   * 함수 헤더
   * 비공개 코드에서 Javadocs
  
> :mag_right: **궁금한 내용이 있거나, 잘 이해되지 않는 내용이 있다면 적어보세요.**
 - 그다지 어려운 내용은 없었습니다.

> :sunglasses: 소감 세줄 요약
 - 코드로 의미를 확인하고, 주석으로 의도를 설명하자  :speech_balloon:
 - 아직도 우리는 이력을 주석으로 기록하고, 닫는 괄호에 주석을 기록하고, 코드 삭제를 주석으로 하고 있다. :vomiting_face:
    * 심지어 git으로 형상을 관리하고 있음에도:nerd_face:
 - 책을 완독하고 나서 부서 품질 담당자와 협의하여 코드 작성 원칙에 대해 재정의 필요. (우선 내가 정리가 먼저 되고 나서:muscle:)  
 
 