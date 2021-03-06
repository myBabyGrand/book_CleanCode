# :pencil: TIL (2022.03.05~2022.03.06)
## DAY 16, 17
:book: 오늘 읽은 범위 : 9장. Unit Test(단위 테스트)
---
> :smile: **책에서 기억하고 싶은 내용을 써보세요.**
 - TDD 법칙 세가지(p.155)
   * **첫째 법칙** : 실패하는 단위 테스트를 작성할 때까지 실제 코드를 작성하지 않는다.
   * **둘째 법칙** : 컴파일은 실패하지 안으면서 실행이 실패하는 정도로만 단위 테스트를 작성한다.
   * **샛째 법칙** : 현재 실패하는 테스트를 통과할 정도로만 실제 코드를 작성한다.

 - 깨끗한 테스트 코드 유지하기(p.156)
   * **테스트 코드는 실제 코드 못지 않게 중요하다.**
   * *테스트는 유연성, 유지보수성, 재사용성을 제공한다.(p.157)*
 - 깨끗한 테스트 코드(p.158)
   * 깨끗한 테스트코드를 만들려면? 세가지가 필요하다. 가독성, 가독성, 가독성.
   * BUILD-OPERATION-CHECK 패턴(p.161)
      + *given-when-then 주석을 달아주는 것과 유사*
    ```
    BUILD : 테스트 자료를 만든다.
    OPERATE : 테스트 자료를 조작한다.
    CHECK : 조작한 결과를 확인한다.
    ```     
   * 도메인에 특화된 테스트 언어(p.161)
   * 이중 표준(p.161)
     + 실제 코드 작성과 동일한 규칙을 가져갈 필요는 없다.
     + 테스트 환경에서 동작하도록 규칙을 변형하여 사용하면 된다.
- 테스트당 assert 하나(p.164) 
   * TEMPLATE METHOD 패턴으로 중복을 제거하면 편리함
   * given, when 부분은 부모class, then은 자식class에서 구현
   * 또는 ```@Before``` 를 이용하는 것도 방법
   * assert문을 꼭 1개로 해야한다는 뜻이 아니로 최소한으로 하라는 뜻
   * *테스트당 개념하나* (p.166)
     + 테스트 함수마다 한 개념만 테스트하라
 - F.I.R.S.T(p.167)
   * **F**ast : 테스트코드는 빨라야 한다. 자주 돌려 볼 수 있게
   * **I**ndependent : 각 테스트는 의존하면 안된다. 한 테스트가 다음 테스트 실행할 환경에 영향(준비)를 해서는 안된다. 테스트간 순서가 영향을 미쳐선 안된다.
   * **R**epetable : 환경과 무관하게 반복 가능해야 한다.
   * **S**elf-Validating : 테스트 결과는 ```boolean``` 값이어야 한다. 
   * **T**imely : 테스트는 적시에 작성해야 한다. 단위 테스트느 테스트하려는 실제 코드를 구현하기 직전에 구현한다.
 - 결론(p.167)

``` 
테스트 코드는 지속적으로 깨끗하게 관리하자. 
표현력을 높이고 간결하게 정리하자
테스트 API를 구현해 도메인 특화 언어(Domain Specific Language, DSL)을 만들자.
```

 
  
> :mag_right: **궁금한 내용이 있거나, 잘 이해되지 않는 내용이 있다면 적어보세요.**
 - TEMPLATE METHOD 패턴
    * *Spring핵심원리 -고급* 강의에서 들었던 내용
    * Spring AOP 구현을 위한 점진적 개발을 하던 과정으로 공통기능(로깅)은 ```abstract```로 구현, 각 비즈니스 class에서 extends 하여 사용하였음
    * [사용했던 tempate code(abstract class)](https://github.com/myBabyGrand/class_Spring04-SpringCoreAdvanced/blob/main/src/main/java/hello/advanced/trace/template/AbstractTemplate.java)
    * 복습겸 정리.
 - 도메인 특화 언어(Domain Specific Language, DSL)
    * [https://ko.wikipedia.org/wiki/도메인특화언어](https://ko.wikipedia.org/wiki/%EB%8F%84%EB%A9%94%EC%9D%B8_%ED%8A%B9%ED%99%94_%EC%96%B8%EC%96%B4)
```
DSL은 간단한 스크립트 언어나 표준 언어로 구현한 API를 가리킨다.
DSL로 짠 코든느 도메인 전문가가 작성한 구조적인 산문 처럼 읽힌다.
좋은 DSL은 도메인 개념과 그 개념을 구현한 코드 사이에 존재하는 '의사소통 간극'을 줄여준다. 
(p.212 시스템은 도메인 특화 언어가 필요하다.)
```
 - 테스트코드에서 말하는 DSL은 도메인에 특화된 테스트 언어를 말한다.
 - 테스트를 위해 구현된 함수와 유틸리티등에 이에 속한다.

> :sunglasses: 소감 세줄 요약
 - 테스트 코드는 작년부터 도입해서 형식적으로나마 작성을 하다 올해부터 code-reviewer 제도가 도입되면서 본격적으로 운영을 해야만 한다. :cowboy_hat_face:
 - 신규 기능은 TDD로 테스트 코드를 무조건 작성하고, 테스트 커버리지는 최대한 높이려고 가이드를 잡는 중이었다. :runner:
 - 물론 위에서 언급한 테스트 코드를 반드시 작성하고, 커버리지를 높이는 것도 중요하지만. 본문에서 언급된 *가독성*, *깨끗한 테스트 코드*, *F.I.R.S.T*를 반영하여 테스트 코드 작성 가이드를 완성해야겠다. :muscle:
 - 여담인지만, 근데 결국 계속 운영 중인 legacy는 JDK 버전부터 막혀서 도입을 하지 않는 걸로 결론났다. 다행인지 불행인지 :scream:
 
 