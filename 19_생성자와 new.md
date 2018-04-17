## 생성자와 new
### 객체
- 객체 : 서로 연관된 변수와 함수를 그룹핑한 그릇
- 프로퍼티(property) : 객체 내의 변수
- 메소드(method) : 객체 내의 함수
```
var person = {}

person.name = 'egoing';
person.introduce = function(){
  return 'My name is '+this.name;
}

document.write(person.introduce());  // My name is egoing
```
> 객체를 만드는 과정에 분산되어 있음

```
var person = {
  'name' : 'egoing',
  'introduce' : function(){
    return 'My name is '+this.name;
  }
}

document.write(person.introduce());
```
> 객체를 정의 할 때 값을 셋팅. 가독성이 좋아지고 중간에 코드가 끼어들 위험성도 사라짐


```
var person1 = {}

person.name = 'egoing';
person.introduce = function(){
  return 'My name is '+this.name;
}

document.write(person.introduce());

var person2 = {}

person.name = 'leezche';
person.introduce = function(){
  return 'My name is '+this.name;
}

document.write(person.introduce());
```
> 이렇게 다른 사람의 이름을 담을 객체가 필요하다면 객체의 정의를 반복해야함. 중복이 일어나면 가독성이 떨어짐, 코드의 양이 많음, 유지보수가 어려워짐

- 이러한 문제로 중복을 해제하기위해 객체의 구조를 재활용할 수 있는 방법이 생성자다.

## 생성자, new
- 생성자의 객체에서 쓸 프로퍼티, 메소드등을 정의하면 new 생성자이름(인자)를 한번 실행 하는 것으로, 인자와 관련된 객체를 만들 수 있음

### 생성자(constructor)
- 객체를 만드는 함수
- 생성자 함수는 일반함수와 구분하기 위해서 첫글자를 대문자로 표시
- 자바스크립트에서 함수는 재사용 가능한 로직의 묶음이 아니라 객체를 만드는 창조자라고 할 수 있음
- 객체 내의 다른 프로퍼티나 메서드를 참조하기위해 this.프로퍼티 와 같이 사용
- 여기에서 `this`는 해당 메소드를 포함하고 있는 변수를 가리킴

### new
- 함수에 new를 붙이면 새로운 객체를 만들어 리턴하고 그 리턴값은 객체가 됨
- 존재하는 함수나 객체를 기반으로 새로운 객체를 만들 때 new를 사용

```
function Person(){}

var p = new Person();
p.name = 'egoing';
p.introduce = function(){
  return 'My name is '+this.name; 
}

document.write(p.introduce()+"<br />");
```
> var p = new Person(); 는 생성자로 var p = {} 와 같다. 즉, 예제에서는 새로운 객체를 변수 p에 담았다.

- 빈 객체를 만드는 것으로 {}과 같지만 var ~ = {} 를 사용하지않고 var ~ = new ~();로 만드는 어떠한 객체(var ~)를 만들때 그 객체가 가지고있어야하는 메소드, 프로퍼티와 같은 데이터를 가지고 우리에게 주어지기 위해서이다.

- 여러사람을 위한 객체를 만든다면
```
function Person(name){
  this.name = name;
  this.introduce = function(){
    return 'My name is '+this.name; 
  }   
}

var p1 = new Person('egoing');
document.write(p1.introduce()+"<br />");
 
var p2 = new Person('leezche');
document.write(p2.introduce());
```
> 초기화(init) : 생성자 내에서 이 객체의 프로퍼티와 메소드를 정의. 재사용성을 높임

- 생성자를 하나 만들어 놓으면 생성자에서 객체를 편하게 찍어낼 수 있다.<br/> 생성자 안에 어떤 속성들이 들어갈지에 대한 속성들을 정의하는 과정을 초기화라고 한다. 객체 초기화 시 동작이 같은 메서드들은 서로 공유되지않고 독립적인 메서드를 생성한다.
