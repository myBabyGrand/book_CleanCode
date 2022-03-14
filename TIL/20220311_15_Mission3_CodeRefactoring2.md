# 원칙1
```
// 본인이 가장 잘하는 언어로(JS, Python 등등) 더러운 코드를 깨끗한 코드로 리팩토링하는 예시를 만들어보세요. 현재 파일은 JS 로 되어있지만. 자유롭게 다른 언어로 변경해주세요. 

// clean code를 읽으면서 기획단계인 개발건을 착수하였다
// 내용인즉 외부 연계모듈로부터 호출되어 수신된 데이터를 통해 결재결과를 처리하고,
// 결재에 관련된 업무모듈을 호출하고 처리 결과를 응답으로 전달하는 동기식 프로그램이다.
// 신입사원때 이미 구현해본 경험이 있는터라, 자신있게 예전의 코드를 열어봤고
// 정말 쓰레기같은 코드가 있었고 그걸 짠게 과거의 나라는 사실에 헛웃음만 나왔다
// clean code를 읽으면서 인상 깊었던 내용을 상기하며,
// 새로운 코드를 복붙했으면 하루 이틀이면 끝날 분량이었지만(프로세스가 예전에 짠거와 거의 유사하다.) 기존 코드를 리팩토링하는 기분으로... 완전히 다른 코드가 나왔다/
// 실제 업무의 코드여서 코드 내용은 작성할 수 없고, pseudo 코드로 대신한다.

// 원칙 1. SOLID의 첫번째, SRP(Single responsibility principle) 단일 책임 원칙 
```

// Before 😣
```JAVA
ApproveBiz.java
public returnVO 연계결재결과수행(paramVO pvo) {
   String 연계ID = pvo.get연계ID();
   if("A".equals(연계ID)){
      상태업데이트를_위한_데이터조합_코드_block;
      수신상태업데이트_코드블록;
     
      A연계특화함수1을_위한_데이터조합_코드_block;
      callA연계특화함수1호출();
      
      결재상태업데이트를_위한_데이터_조합_코드_block;
      this.결재상태업데이트();

      A연계특화함수2을_위한_데이터조합_코드_block;
      callA연계특화함수2호출();
      
      결재업무후처리함수호출을_위한_데이터조합_코드_block; 
      this.결재업무후처리함수호출();
   }else if()"A".equals(연계ID){
     ... 후략
   }
  return returnVO;
}
```
// 무엇을 고치려고 하는지, 고치려는 문제가 무엇인지 알려주세요.
 - 문제는 이것을 수행하는 ApproveBiz 라는 클래스가 너무 컸다. 
 - 결재를 처리하는 class 이긴 하지만, 하는 일이 너무 방대했다.
 - 코드 길이는 1만줄에 달했고, 이 거대한 클래스가 더 거대해지는걸 거들고 싶진 않았다


// After 😎
```JAVA
ExternalApproveResultRecevieBiz.java
public returnVO A연계결재결과수행 (paramVO pvo) {
   
  상태업데이트를_위한_데이터조합_코드_block;
  this.수신상태업데이트();
 
  A연계특화함수1을_위한_데이터조합_코드_block;
  callA연계특화함수1호출();
  
  결재상태업데이트를_위한_데이터조합_코드_block;
  this.결재상태업데이트();

  A연계특화함수2을_위한_데이터조합_코드_block;
  callA연계특화함수2호출();
  
  결재업무후처리함수호출을_위한_데이터조합_코드_block; 
  this.결재업무후처리함수호출();
   
  return returnVO;
}
```

  
// 어떻게 고쳤는지, 사례에서 무엇을 배워야 하는지 설명해주세요.
```
그래서 클래스를 찢었다. 
연계결재결과만 처리하는 ExternalApproveResultRecevieBiz class를 새로 만들었다.
SOLID의 
  I (ISP, Interface segregation principle 인터페이스 분리 원칙)
  D (DIP Dependency inversion principle 의존관계 역전 원칙)
를 생각해서 interface나 abstrace class를 도입하고 싶었다. 
그래서 다른 연계건들을 처리하는 프로그램을 이것을 implement나 extends 해서 사용하도록 고치고 싶었으나, 우선 Best practice class를 만드는 걸로 만족하였다. 
한 번에 너무 많은 걸 하려다간 하나도 못하는 경우가 있어 점진적으로 개선하고자 한다.
```

# 원칙2
--- 
```
// 본인이 가장 잘하는 언어로(JS, Python 등등) 더러운 코드를 깨끗한 코드로 리팩토링하는 예시를 만들어보세요. 현재 파일은 JS 로 되어있지만. 자유롭게 다른 언어로 변경해주세요. 

// 원칙 1에서 이어집니다.
// 원칙 2. SOLID의 OCP(Open/closed principle),	개방-폐쇄 원칙 
```

// Before 😣
```JAVA
ExternalApproveResultRecevieBiz.java
public returnVO A연계결재결과수행 (paramVO pvo) {
   
  상태업데이트를_위한_데이터조합_코드_block;
  this.수신상태업데이트();
 
  A연계특화함수1을_위한_데이터조합_코드_block;
  callA연계특화함수1호출();
  
  결재상태업데이트를_위한_데이터조합_코드_block;
  this.결재상태업데이트();

  A연계특화함수2을_위한_데이터조합_코드_block;
  callA연계특화함수2호출();
  
  결재업무후처리함수호출을_위한_데이터조합_코드_block; 
  this.결재업무후처리함수호출();
   
  return returnVO;
}
```

// 무엇을 고치려고 하는지, 고치려는 문제가 무엇인지 알려주세요.
 - 데이터조합 코드 block은 적게는 2-3줄, 많게는 15줄 정도된다.
 - 실제로는 이안에서 DB를 갔다와서 데이터를 정리하는등 코드 블록에서 꽤 많은 일들이 벌어진다.
 - 이 부분을 다른 연계가 추가되면 똑같은 코드에 변수값만 변경된다.
 - 따라서 이런 부분은 확장성을 고려해 별도의 메서드(함수)로 추출했다

// After 😎
```JAVA
ExternalApproveResultRecevieBiz.java
public returnVO A연계결재결과수행 (paramVO pvo) {
  ApproveBiz approveBiz = new ApproveBiz();
  
  상태업데이트를_위한_데이터조합_함수;
  this.수신상태업데이트();
 
  A연계특화함수1을_위한_데이터조합_함수;
  callA연계특화함수1호출();
  
  결재상태업데이트를_위한_데이터조합_함수;
  approveBiz.결재상태업데이트();

  A연계특화함수2을_위한_데이터조합_함수;
  callA연계특화함수2호출();
  
  결재업무후처리함수호출을_위한_데이터조합_함수; 
  approveBiz.결재업무후처리함수호출();
   
  return returnVO;
}

private void 상태업데이트를_위한_데이터조합_함수(paramVO pvo){
  pvo.set속성1(...후략);
}
private void 수신상태업데이트(paramVO pvo){
  
}
private void 결재상태업데이트를_위한_데이터조합_함수(paramVO pvo){
  pvo.set속성2(...후략);
}

private void A연계특화함수1을_위한_데이터조합_함수(paramVO pvo){
  pvo.set속성2(...후략);
}

후략
```

// 어떻게 고쳤는지, 사례에서 무엇을 배워야 하는지 설명해주세요.
 - 공통적으로 데이터 조합을 하는 코드 블록은 모두 메서드로 추출하였다.
 - 어떤 신규 연계가 오더라도 해당 메서드 내에서 처리 가능하도록 확장성을 고려하여 작성한다.
 - 신규 기능이 필요하다면 새로운 메서드로 작성 하도록 함수명 작명에 고민을 많이하였다.
 - 각 연계특화기능을 위한 함수는 확장을 할 수 있다면 명칭에 A연계라는 단어를 빼 확장할 수 있도록 하였고, 그렇지 않고 A연계 고유의 기능은 A연계 단어를 붙여 고유 기능임을 명시하였다.

---

# 원칙3
```
// 본인이 가장 잘하는 언어로(JS, Python 등등) 더러운 코드를 깨끗한 코드로 리팩토링하는 예시를 만들어보세요. 현재 파일은 JS 로 되어있지만. 자유롭게 다른 언어로 변경해주세요. 


// 원칙 2에서 이어집니다.
// 원칙 3. 좋은 주석
   * 법적인 주석
   * 정보를 제공하는 주석
   * 의미를 설명하는 주석
   * 의미를 명료하게 밝히는 주석
   * 결과를 경고하는 주석
   * TODO 주석
   * 중요성을 강조하는 주석
   * 공개 API에서 Javadocs
// 나쁜코드에 주석을 달지마라. 새로짜라
```

// Before 😣
```JAVA
ApproveBiz.java
public returnVO 연계결재결과수행(paramVO pvo) {
   String 연계ID = pvo.get연계ID();
   if("A".equals(연계ID)){
      /*상태 업데이트를 위해 데이터를 가져와서 셋팅*/
      상태업데이트를_위한_데이터조합_코드_block;
      /*수신 상태 갱신 시작*/
      수신상태업데이트_코드블록;

      /*A연계 ~~ 한 특화기능이 있어 ~~ 에서 데이터를 가져와야 한다*/     
      A연계특화함수1을_위한_데이터조합_코드_block;
      /*A연계 특화 기능 시작*/
      callA연계특화함수1호출();

      /*결재 상태를 위해 데이터 가져옴*/
      결재상태업데이트를_위한_데이터_조합_코드_block;
      this.결재상태업데이트(approveId, "Y","Y","");//결재ID, 정상수신YN, 수신상태정상여부YN, 기타메시지

      /*A연계 ~~ 한 특화기능2를 위한 데이터를 처리*/     
      A연계특화함수2을_위한_데이터조합_코드_block;

      /*A연계 특화 기능 시작2*/     
      callA연계특화함수2호출();
      
      결재업무후처리함수호출을_위한_데이터조합_코드_block; 
      this.결재업무후처리함수호출();
   }else if()"A".equals(연계ID){
     ... 후략
   }
  return returnVO;
}
```

// 무엇을 고치려고 하는지, 고치려는 문제가 무엇인지 알려주세요.
 1. 주석이 함수 시작전에 내용을 일일이 설명한다.
 2. 변수를 3개이상 사용하는 함수가 있어 호출시 주석을 달아야만 했다.
 3. 기타 불필요한 주석이 너무 많고 설명을 위한 설명의 주석도 있다
  
  

// After 😎
```JAVA
ExternalApproveResultRecevieBiz.java

//TODO ENUM을 사용해 A연계외 다른 연계건 처리에도 활용해보자
static final String RECEIVE_SUCCESS_Y = "Y";
static final String RECEIVE_SUCCESS_N = "N";
static final String RECEIVE_STATUS_UPDATE_SUCCESS_Y = "Y";
static final String RECEIVE_STATUS_UPDATE_SUCCESS_N = "N";

//TODO A연계외 다른 연계건 처리 확장을 위해 interface나 abstract 로 구현할 것을 고민 해보자.
public returnVO A연계결재결과수행 (paramVO pvo) {
  ApproveBiz approveBiz = new ApproveBiz();  
  
  initDataForA연계ApproveReceiveStatus(pvo);
  updateApproveReceiveStatus(pvo);

  setDataForAddFuntion1ForA연계(pvo);
  excuteAddFunctionForA연계(pvo)
  
  setDataForApproveStatusUpdate();
  approveBiz.결재상태업데이트(approveId
                     ,RECEIVE_SUCCESS_Y
                     ,RECEIVE_STATUS_UPDATE_SUCCESS_Y);

  setDataForAddFuntion2ForA연계();
  if(isByBatchCountOver(pvo)){
    //배치 JobId : ApproveReceiveBulkBIZ
    return setApproveReturn();
  }
  
  setDataForApproveReceiveAfterProcess();
  approveBiz.결재업무후처리함수호출();
   
  return returnVO;
}

private void initDataForA연계ApproveReceiveStatus(paramVO pvo){
  pvo.set속성1(...후략);
}

private void updateApproveReceiveStatus(paramVO pvo){
  
}

private void setDataForAddFuntion1ForA연계(paramVO pvo){
  pvo.set속성2(...후략);
}

private void setDataForAddFuntion2ForA연계(paramVO pvo){
  pvo.set속성2(...후략);
}
후략
```

  
// 어떻게 고쳤는지, 사례에서 무엇을 배워야 하는지 설명해주세요.
 - 설명하는 주석은 배치프로그램으로 처리할 건수인 경우 사용되는 배치프로그램 명뿐
 - 모든 함수명는 서술형으로 직관적으로 이해할 수 있도록 작성
 - TODO주석 를 통해 추가 개선 방향을 작성
 - 변수가 3개이상으로 호출하는 함수는 직접 고치진 못하였고(영향도가 큰 함수라) 대신 static final 상수로 상수명을 보고 바로 이해할 수 있도록 고쳤다.





