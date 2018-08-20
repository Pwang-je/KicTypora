---
Date : 1028-08
Language : JavaScript
---



[TOC]



## Array

### 배열의 앞과 뒤에서 엘리먼트 추가하거나 삭제하기.

```javascrip
.push(element) : 배열의 뒤에 엘리먼트 추가
.pop () : 배열의 뒤에서 엘리먼트 삭제하고 리턴
.shift() : 배열의 앞에서 엘리먼트 삭제하고 리턴
.unshift(element) : 배열의 앞에 엘리먼트 추가
```



### 배열 붙이기, 검색하기

```javascript
arr1.concat(arr2) : arr1 과 arr2 붙임
arr.indexof(element) : arr 에서 element 가 있는 첫 위치를 검색
arr.lastindexof(element) : arr 에서 element 가 있는 마지막 위치를 검색
```



### 문자열 split 함수

```javascript
// code
var str = "1,2,3,4,5";
arr = str.split(",");

// result
arr = ["1","2","3","4","5"];
```



## If, Case, While, do while, For, For in



### Case

```javascript
// javascript 의 case 에서는, 여러개를 한번에 넣을 때,

function daysInMonth( month ){
  switch(month){
    case 2:
      return 28;
      break;
    case 4,6,9,11:
      return 30;
    default:
      return 31;    }
}

// 가 아닌, 

function daysInMonth( month ){
  switch(month){
    case 2:
      return 28;
    case 4:
    case 6:
    case 9:
    case 11:
      return 30;
    default:
      return 31;    }
}

// 이런식으로 여러개의 값을 한 번에 처리하려면 case 를 여러번 적어 줘야 함.
```



### do while

```javascript
do{
    /* 반복 실행될 코드 */
}while( /*조건식*/ );
       
// do 가 실행되고 난 후 while 의 조건식을 보고 판단함.
```



### For in

```javascript
var obj = {
  name: "object",
  weight: 30,
  isObject:true,
  arr:[1,2,3],
  obj:{property:1}
};

object.keys(obj);
// 결과
["name","weight","isObject","arr","obj"]

// -> object.keys(변수) 는 해당 변수가 가진 object가 무엇인지를 반환한다.





```

