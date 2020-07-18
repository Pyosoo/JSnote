# ※변수선언 var
- - -

ES5 까지는 유일한 변수 선언은 var로 했다.   
하지만 많은 문제가 있었다.(JS가 저급언어라고 취급받았던 ES5 이전시절에 한몫을 한것이라고 한다)   

### 1. 함수 스코프의 var   
```
for(var i = 0; i<10; i++){
  console.log(i);
)

console.log(i); // 10
```
위 처럼 for문을 끝나고 i라는 변수는 남아있다.. 전체를 갖는 function스코프를 기준으로 갖고있기 때문이다.   

### 2. 호이스팅   
그 변수가 속한 스코프의 최상단으로 끌어올려지는 것을 호이스팅(Hoisting)이라고 부른다.   
```
console.log(Myvar); //undefined
var Myvar = 1;
```
위 코드는 오류가 나질 않는다.  하지만 Myvar는 undefined 값을 가지게 된다.   
다음 처럼 실행되기 때문이다.   
```
var Myvar = undefined;
console.log(Myvar);
Myar = 1;
```

### 3. 그 외   
var 변수는 재정의가 가능하다. ```{ var a=1; var a=2; }```   
이는 직관적이지 않으며 버그로 이루어질 수 있다.   

