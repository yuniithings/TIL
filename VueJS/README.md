# Majesty of vuejs

# chapter1

### tutorial
- vue의 el 옵션을 이용하여 엘레멘트를 선택한다.
- {{ }}로 데이터 바인딩
<br/>( {{ }} 안의 값들은 javascript 코드로 읽히며, {{ 1+2 }}의 경우에 화면에 3으로 표시된다. )

##### 2017. 11. 30
---
# chapter 2

### v-model
- v-model:: direcitve를 통하여 양방향 바인딩이 가능하다.
<br/>( 데이터 모델과 - 사용자가 입력한 값이 동적으로 변경됨 )

##### 2017. 11. 30
---
# chapter 3

### directive
- v-if/else :: 토글 비용이 높다. 런타임 조건이 자주 변경되지 않을때 사용
<br/>( false조건은 초기 렌더링 시 읽지 않기 때문에 초기 렌더링 비용이 낮다. )
- v-show :: 초기 렌더링 비용이 높다. 자주 토글하는 경우에 사용

##### 2017. 11. 30
---
# chapter 4

### list-redering

- v-for :: item in array 의 형식.
<br/>v-for="(value, index) in array" OR v-for="(value, key, index) in array" 와 같이 key값 혹은 index값도 해당 scope 내에서 사용 할 수 있다.

##### 2017. 11. 30
---
# chapter 5

### event-handler

- v-on :: event listener를 생성합니다.
<br/>( v-on:key="cnt++" )


##### 2017. 11. 30
---
