# ※this
- - -

#### Javascript의 this   
JS의 this 는 다른 언어의 this와는 좀 다르다.   
```
int main {
  void Sayhi(){
    cout << this.name;
  }
```
다음과 같은 C++코드는 오류가 생긴다. 그 이는 this가 무엇을 참조하는지 모르기 떄문이다..   
하지만 JS의 this는 이것이 가능하다.   
```
function Sayhi(){
  alert(this.name);
}
```
그 이유는 JS의 this값은 **런타임**에 결정이 되기 떄문이다!   
```
 **장점 = 함수 하나를 가지고 여러 객체에서 재사용을 할 수 있다.**     
**단점 = 위와같은 유연성때문에 실수를 유발하기 쉽다.**     
```

```
let user1 = {name : "ps";}
let user2 = {name : "ys";}

function sayhi(){
  alert(this.name);
}

user1.f = sayhi; // ps 출력
user2.f = sayhi; // ys 출력
```

객체 없이 호출을 할 수도 있다. 하지만 이는 **엄격 모드(use strict)** 와 관련이 있으므로 다음에 다루겠다.   


#### **'this'** 가 없는 화살표 함수
화살표함수는 일반함수와는 달리 고유의 'this'를 갖지 않는다.   
화살표 함수에서 this를 참조하게 되면, 다른 평범한 외부 함수에서 this값을 가져온다.   
```
let user = {
  firstName: "보라",
  sayHi() {
    let arrow = () => alert(this.firstName);
    arrow();
  }
};

user.sayHi(); // 보라
```

# ※ this 바인딩
- - -
Javascript에서 this 때문에 좀 혼잡한 부분이 있다.   
C++에서 this를 사용할 땐 this의 주최가 되는 것이 명확했어서 헷갈릴 것이 별로 적었지만,   
JS에서는 아무때나 this를 사용할 수 있다.   
```
function sum = (a,b) => {
  return this.a + this.b;
}
```
다음과 같은 코드에서 this는 누구를 가르킬까?   
객체없이 호출되는 경우에는 **전역 객체** 가 바인딩 되는데, 브라우저 환경에서는 window객체가 바인딩된다.   

```
function Something(){
  this.value = 1;
  setInterval(function increase(){
     this.value++;
     },1000);
 }
 const obj = new Something();
 ```
 실행해보면 의도와 달리 obj.value는 증가하지 않는다.  setInterval 핫무의 인자로 들어간 increase함수는    
 전역환경에서 실행되기 때문에 this는 window객체를 참조한다.   
 
 + 해결법1(클로저)    
 ```
 function Somethin(){
  this.value = 1;
  var that = this;
  setInterval(function increase(){
    thiar.value++;
  },1000);
}
const obj = new Something();
//미리 저장해둔 that변수를 통해 this객체에 접근한다.   
 ```
 
+ 해결법2 (화살표함수)   
 ```
 function Something(){
  this.value = 1;
  setInterbal( () => {
    this.value++;
   },1000);
 }
 const obj = new Something();
 // 화살표함수를 사용했기 때문에 this는 setInterval의 동작과는 상관없이 obj를 참조한다. setInterval은 브라우저의 함수임으로 기본 this가 브라우저였던 것인데    
 // function함수로 감싸져있고 화살표함수를 사용함으로써 이를 바꿔준 것 같다.
 ```
 ### 클로져(closure)   
 ES5에선 위와같은 문제를 해결하기 위해 클로져를 사용했다.   
 클로저는 함수가 생성되는 시점에 접근 가능했던 변수들을 생성 이후에도 계속해서 접근할 수 있게 해주는 기능이다.   
 
 ```
 function makeAddFunc(x){
  return function add(y) {
    return x + y;
    };
 }
 // add 함수는 상위 함수인 makeAddFunc의 매개변수 x에 접근할 수 있다.    
 ```
