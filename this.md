# this
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

객체 없이 호출을 할 수도 있다. 하지만 이는 **엄격 모드(use strict)**와 관련이 있으므로 다음에 다루겠다.   


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

