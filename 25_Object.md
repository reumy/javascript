## Object
- 객체의 가장 기본적인 형태를 가지고 있는 객체
- 아무것도 상속받지 않는 순수한 객체
- 값을 저장하는 기본적인 단위
- 모든 객체는 Object 객체를 상속받으므로 모든 객체는 Object 객체의 프로퍼티를 가지고 있음

## 메소드 사용법의 차이 (prototype의 유무)
### Object.keys() - _(prototype X)_
- 객체가 가진 key값을 리턴
```
var arr = ['a','b','c'];
console.log(Object.keys(arr));  // ["0", "1", "2"]
```
> 인자에 사용할 배열을 넣어줌<br/>실행 : Object.메소드(인자);

### Object`.prototype`.toString() - _(prototype O)_
- 객체가 담고있는 값을 보기좋게 출력
```
var o = new Object();
console.log(o.toString());  // [object object]

var a = [1, 2, 3]
console.log(a.toString());  // 1,2,3

var b = new Array(1,2,3);
console.log(b.toString());  // 1,2,3
```
> prototype이 붙어있는 메소드들은 새로운 객체를 만들어주고 실행<br/>실행 : 객체가 담긴 식별자.메소드();

- prototype이 있는 메소드가 new Object()를 한다는건 Object가 생성자 함수임을 의미
```
즉,

Object.keys()는
Object.keys = function(){~} 형태

Object.prototype.toString()은
Object.prototype.toString = function(){~} 형태
```

## Object 확장
- 모든 객체가 사용할 수 있는 메소드를 추가하기
- Object는 모든 객체의 부모이기때문에 Objcet를 확장해 메소드를 만들면 그 메소드는 모든 객체들이 사용할 수 있다.

```
Object.prototype.contain = function(neddle) {
  for(var name in this){
    if(this[name] === neddle){
      return true;
    }
  }
  return false;
}

var o = {'name':'egoing', 'city':'seoul'}
console.log(o.contain('egoing'));  // true

var a = ['egoing','leezche','grapittie'];
console.log(a.contain('leezche'));  // true
```
> 해당 인자를 찾아서 있으면 true 없으면 false를 리턴<br/>this : 메소드가 소속 된 객체인 o 와 a


## Object 확장의 위험
- Object 객체는 확장하지 않는 것이 바람직한 이유는 모든 객체에 영향을 주기 때문
```
for(var name in o){
  console.log(name);  // name city contain
}
```
> 확장한 프로퍼티인 contain이 포함된다.

- 위 문제를 해결하기위해 hasOwnProperty를 사용함
`hasOwnProperty : 프로퍼티 해당 객체의 소속인지를 체크`
```
for(var name in o){
  if(o.hasOwnProperty(name)){
    console.log(name);  // name city
  }
}
```
> hasOwnProperty는 인자로 전달된 속성의 이름이 hasOwnProperty가 실행되고있는 해당 객체의 직접적인 속성인지 여부를 판단하여 만약 prototype으로 상속받은 객체라면 false가 된다. 
