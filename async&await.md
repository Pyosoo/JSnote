# ※ Async와 Await 
- - -

ES5의 콜백함수, ES6의 프로미스 와 같은 함수는 모두 비동기 프로그래밍을 위한 것들이다.    
비동기 프로그래밍이란? 요청에대한 응답을 기다리지않고 백그라운드에서 실행되기 때문에 기존로직을 방해하지 않고 동시에 작동할 수 있게 진행되는 것이다.   
반대로 동기 프로그래밍이란 요청에 대한 응답이 올때까지 마냥 기다리는 것이다. 그렇게 되면 오류가 발생하거나 시간이 오래 걸렸을 때 그만큼의 손해가 있을 것이다.   

그 중 프로미스 다음으로 async await가 있다.   
then 메서드를 체인형식으로 호출하는 것보다 가독성이 좋아진다.   
하지만 async await가 프로미스를 완전히 대체하는 것은 아니다.  엄연히 보면 Promise 가 async await보다 큰 개념이다.   

### ■특징1   
**async await 함수는 프로미스를 반환한다**    
```
async function getData(){
  return 123;
}
getData().then(data => console.log(data)); //123출력
```
123 숫자를 반환하는 것 같지만, 프로미스를 반환했기에 then 메서드를 사용했다.   


### ■특징2   
**await 키워드는 async 키워드 없이 사용할 수 없다.**   
```
function getData(){ 
  const data = await requestData(10);
  console.log(data);
}
//에러
```


### ■특징3
**async await는 프로미스보다 가독성이 좋다.**   
다음 두 함수는 각각 프로미스와 async await로 구현된 것이다. 어떠한 것이 더 가독성이 좋은지 판단해보기 바란다.   
```
function getDataPromise(){
  asyncFunc1()
    .then(data => {
      console.log(data);
      return asyncFunc2();
     })
    .then(data => {
      console.log(data);
     });
}

async function getDataAsync(){
  const data1 = await asyncFunc1();
  console.log(data1);
  const data2 = await asyncFunc2();
  console.log(data2);
}
```
비동기 함수간의 의존성이 높아질수록 프로미스와 async await와의 가독성 차이는 커진다.   


## ※ 활용하기   
- - -

### 비동기 함수를 병렬로 실행하기
```
aysnc function getData() {
  const data1 = await asyncFunc1();
  const data2 = await asyncFunc2();
}
```
 앞의 코드에서 Func1이 끝날때 까지 Func2는 실행할 수 없다.   
 하지만 두 함수 사이의 의존성이 없다면 같이 실행시키는 것이 좋다.   
```
async funtion getData(){
  const p1 = asyncFunc1();
  const p2 = asyncFunc2();
  const data1 = await p1;
  const data2 = await p2;
}

//Promise.all을 사용해서 더 간단하게
async function getData(){
  const [data1, data2] = await Promise.all([asyncFunc1(), asyncFunc2()];
  //...
}
```
```
두 개의 프로미스를 먼저 생성하고 await 키워드를 나중에 사용하면 병렬로 실행하는 코드가 된다.   


### 예외 처리   
async await 함수 내부에서 발생하는 예외는 try catch문으로 처리하는 게좋다
```
async function getData(){
  try{
    await doAsync();
    return doSync();
   }catch(error){
    console.log(error);
   }
 }
 ```  
 만약 getData함수가 async await함수가 아니었다면 doAsync 함수에서 발생하는 예외는 catch에서 처리되지 않는다.   
 doAysnc함수의 처리가 끝나는 시점을 알 수 없기 때문이다.   
 
 
