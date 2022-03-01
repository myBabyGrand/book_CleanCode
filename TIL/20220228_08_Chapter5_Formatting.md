
# :pencil: TIL (2022.02.28)
## DAY 11
:book: 오늘 읽은 범위 : 5장. Fomatting(형식 맞추기)
---
> :smile: **책에서 기억하고 싶은 내용을 써보세요.**
- 적절한 행 길이를 유지하라(p.96)
   * 신문 기사처럼 작성하라(p.98)
   ```
   신문은 다양한 기사로 이뤄진다. 대다수 기사가 아주 짧다. 어떤 기사는 조금 길다.
   한 면을 채우는 기사는 거의 없다. 신문이 읽을만한 이유는 여기에 있다.
   ```
   * 개념은 빈 행으로 분리하라(p.98)
   * 세로 밀집도(p.100)
   
   ``` 서로 밀접한 코드 행은 세로로 가까이 놓여야 한다는 뜻이다. ```
   * 수직 거리(p.101)
     + 변수선언 : 변수는 사용하는 위치에 최대한 가까이 선언한다.
     + 인스턴스 변수 : 클래스 맨 처음에 선언한다.
     + 종속함수 : 한 함수가 다른 함수를 호출한다면 두 함수는 세로로 가까이 배치한다.
     + 개념적 유사성 : 친화도가 높을수록 코드를 가까이 배치한다.
   * 세로 순서(p.106)
      + 일반적으로 함수 호출 종속성은 아래 방향으로 유지한다.(호출되는 함수는 호출하는 함수보다 나중에 배치한다.)
      + 고차원->저차원 (두괄식?)
 - 가로 형식 맞추기(p.107) : 한 행은 max 120자가 적절
   * 가로 공백과 밀집도(p.108)
     + 할당 연산자(=, += 등)은 앞뒤 공백
     + 함수와 인수는 공백X
     + 함수를 호출하는 코드에서 괄호 안 인수도 공백으로 분리
     + 수식에서는 항 사이에는 공백O, 승수에는 공백X
   * 가로 정렬(p.109) : 불필요
   * 들여쓰기(p.111)
 - 팀 규칙(p.113)
 
  
> :mag_right: **궁금한 내용이 있거나, 잘 이해되지 않는 내용이 있다면 적어보세요.**
 - scissors rule (가위 규칙) (https://blog.eq8.eu/article/scissors-rule-in-coding.html#:~:text=The%20rule%20is%20from%20old,it%20with%20scissors%20in%20half.)
```
The rule is from old days where programers where styling the code in a way that public methods / interface methods were at the top of the code and private methods were at the bottom. 
So if you theoretically print the source code of a file and you can cut it with scissors in half. 
This way you will end up with list of public methods so that other programers / developers can implement them in their code.
``` 
> :sunglasses: 소감 세줄 요약
 - 포맷터에 대한 가이드, 부서에서 사용중인 포맷터를 점검해보자
 - 포맷터가 일으킨 다른 문제에 대해서도 팀원들과 상의 해보자
    * 신규 프로젝트와 함께 도입된 포맷터가 기존 프로젝트에 영향을 줬다.
 - 포맷터를 renewal 해보자. :muscle:
 
 