# :pencil: TIL (2022.03.01)
## DAY 12
:book: 오늘 읽은 범위 : 6장. Objects and Data Structure(객체와 자료구조)
---
> :smile: **책에서 기억하고 싶은 내용을 써보세요.**
 - 자료 추상화(p.118)
 - 자료/객체 비대칭(p.119)
```
 (자료 구조를 사용하는)절차적인 코드는 기존 자료 구조를 변경하지 않으면서 새 함수를 추가하기 쉽다.
반면, 객체 지향 코드는 기존 함수를 변경 하지 않으면서 새 클래스를 추가하기 쉽다.

 절차적인 코드는 새로운 자료 구조를 추가하기 어렵다. 그러려면 모든 함수를 고쳐야 한다. 
객체 지향 코드는 새로운 함수를 추가하기 어렵다. 그러며면 모든 클래스를 고쳐야 한다.
```
 - 디미터법칙(p.123)
   * 모듈은 자신이 조작하는 객체의 속사정을 몰라야 한다는 법칙.
   * ```클래스 C의 메서드 f는 다음과 같은 객체의 메서드만 호출해야 한다.```
     + 클래스C
     + f가 생성한 객체
     + f 인수로 넘어온 객체
     + C 인스턴스 변수에 저장된 객체
   * 기차 충돌(p.123)
   ```JAVA
   final String outputDir = ctxt.getOptions().getScrathDir().getAbsolutePath();

   //아래와 같이 나눌 수 있다.
   Options opts = ctxt.getOptions();
   File scratchDir = opts.getScratchDir();
   final String outputDir = scratchDir.getAbsolutePath();
   ```
   * 객체라면 내부 구조를 숨겨야 하므로 위반, 자료 구조라면 내부 구조를 노출 하므로 디미터 법칙 적용 대상이 아님
   * 아래와 같이 표현되었다면 혼란이 없었을 것이다.  
   ```JAVA
    final String outputDir = ctxt.options.scratchDir.absolutePath 
   ``` 
   * 자료구조는 무조건 함수 없이 공개 변수만 포함
   * 객체는 비공개 변수와 공개함수를 포함해야 함.
   * 잡종 구조(p.124)
     + 자료구조에도 조회 함수와 설정 함수를 정의하라는 요구하는 프레임워크와 표준(빈 bean)이 존재한다.
   * 구조체 감추기(p.125)
   * 위의 예시의 ```outputDir``` 아래 예시와 같이 사용됨
   ```JAVA   
    String outFile = outputDir + "/" + className.replace('.', '/') + ".class"; 
    FileOutputStream fout = new FileOutputStream(outFile); 
    BufferedOutputStream bos = new BufferedOutputStream(fout);
   ```
   * 그렇다면 아래와 같이 refactoring이 가능하다
   ```JAVA   
    BufferedOutputStream bos = ctxt.createScratchFileStream(className);
   ```
 - 자료 전달 객체(Data Transfer Object, DTO)(p.126)
   * 활성 레코드(p.127)
      + DB나 다른 소스에서 자료를 직접 반환한 결과물
      + 자료 구조로 취급한다. 
      + 비즈니스 규칙을 담으면서 내부 자료를 숨기는 객체를 따로 생성한다.
  
> :mag_right: **궁금한 내용이 있거나, 잘 이해되지 않는 내용이 있다면 적어보세요.**
 - [Heuristic 휴리스틱 on wikipedia](https://ko.wikipedia.org/wiki/%ED%9C%B4%EB%A6%AC%EC%8A%A4%ED%8B%B1_%EC%9D%B4%EB%A1%A0#:~:text=%ED%9C%B4%EB%A6%AC%EC%8A%A4%ED%8B%B1(heuristics)%20%EB%98%90%EB%8A%94%20%EB%B0%9C%EA%B2%AC%EB%B2%95(,%EA%B0%84%ED%8E%B8%EC%B6%94%EB%A1%A0%EC%9D%98%20%EB%B0%A9%EB%B2%95%EC%9D%B4%EB%8B%A4.))
```
휴리스틱(heuristics) 또는 발견법(發見法)이란 불충분한 시간이나 정보로 인하여 합리적인 판단을 할 수 없거나, 
체계적이면서 합리적인 판단이 굳이 필요하지 않은 상황에서 
사람들이 빠르게 사용할 수 있게 보다 용이하게 구성된 간편추론의 방법이다.
``` 
> :sunglasses: 소감 세줄 요약
 - 갑자기 훅 어려워진 느낌
 - 자료 구조 vs 객체 취급을 코드로 구현해보자.(주제만 정하면 바로 고) :muscle:
 - 객체를 구현하는 코드에 대해서는 매우 깐깐한 잣대를 대는 경우가 많았는데 자료 구조에 대해서는 어떠하였는지 생각해보자.
 
 