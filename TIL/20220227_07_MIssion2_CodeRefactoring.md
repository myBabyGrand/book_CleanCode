https://replit.com/@myBabyGrand/GlamorousPlaintiveNotification-3#mission1.js
//Mission 1
// BAD 더러운 코드 😣
// Hint❕ : 검색하기 쉬운 이름을 사용하세요.
// blastOFF는 로켓 발사를 의미. 86400000은 하루의 밀리초 (milliseconds) 의미. 

// What the heck is 86400000 for?
```JAVASCRIPT
setTimeout(blastOff, 86400000);
```

// GOOD 😎
// 위 코드를 깨끗하게 다시 작성해 주세요.
```JAVASCRIPT
const oneDayMilliSec = 24 * 60 * 60 * 1000;
setTimeout(blastOff, oneDayMilliSec);
```

// 어떻게 고쳤는지, 사례에서 무엇을 배워야 하는지 설명해주세요.
코드를 보고 의미를 바로 유추할 수 있게 구현해야 한다. 
검색이 용이한 이름을 사용해야 한다.

----
// Mission 2
// BAD 더러운 코드 😣
// Hint❕ : 의미있는 이름을 사용해주세요.
```JAVASCRIPT
const yyyymmdstr = moment().format("YYYY/MM/DD");
```

// GOOD 😎
// 위 코드를 깨끗하게 다시 작성해 주세요.
```JAVASCRIPT
const nowYyyyMmDd = moment().format("YYYY/MM/DD");
```

// 어떻게 고쳤는지, 사례에서 무엇을 배워야 하는지 설명해주세요.
의미있는 명사(now)와 이름이 표현하는 내용(yyyymmdd의 형식)으로 이름 변경


---
//Mission 3
// BAD 더러운 코드 😣
// Hint❕ : 불필요하게 반복하지 마세요.
```JAVASCRIPT
const Car = {
  carMake: "Honda",
  carModel: "Accord",
  carColor: "Blue"
};

function paintCar(car, color) {
  car.carColor = color;
}
```

// GOOD 😎
// 위 코드를 깨끗하게 다시 작성해 주세요.
```JAVASCRIPT
const Car = {
  make: "Honda",
  model: "Accord",
  color: "Blue"
};

function paintCar(car, color) {
  car.color = color;
}
```

// 어떻게 고쳤는지, 사례에서 무엇을 배워야 하는지 설명해주세요.
Car라는 객체의 속성들이 car~로 시작하는 속성이름을 가진다.
이미 Car라는 객체에 속한 속성임을 알 수 있으므로 불필요한 접두어다.(삭제)