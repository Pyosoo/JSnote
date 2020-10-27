# subStr && subString && padStart !
- - -
## 1. subStr
```
let str = "abcde";
console.log(str.subStr(1,3)); // bcd 
```
(startIndex, 개수)


## 2. subString
```
let str = "abcde";
console.log(str.subString(1,2)) // bc
```
(stringIntedx, endIndex)

## 3. padStart
원하는 자리수만큼을 만족시키는 문자열을 만족시킨다. 
예를 들어 9를 2진법으로 바꾸면 1001(2)가 된다. 하지만 5자리 인 01001(2)를 원한다면
```
let a = 9;
console.log(a.toString(2).padStart(5,0)); // 01001
```
처럼 된다.

