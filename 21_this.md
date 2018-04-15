## this
- 함수 내에서 함수 호출 맥락(context)을 의미
- 맥락 : 상황에 따라서 달라진다는 의미
- 가변적으로 함수를 어떻게 호출하느냐에 따라 가리키는 대상이 달라짐

## 함수호출
- 함수안에 this는 그 함수가 소속된 객체를 가르킴
```
function func(){
  if(window === this){
  document.write("window === this");
  }
}

func(); 
```
- 결과
```
window === this 즉, window === this가 true이므로 실행이 돼서 window === this를 출력
```
> this는 전역객체인 window와 같다.
