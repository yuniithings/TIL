# Calendar.es5.js

## ES5 기반으로 작성된 클래스이며 별도의 CSS 템플릿이 필요합니다.
### table tag 기반으로 작성되었으며, 적용가능한 클래스 목록입니다.

- table / table-bordered / table-calendar : 테이블 객체에 적용된 클래스이며
renderCalendar: function 내에서 클래스를 수정하여 사용 가능합니다.

- thead는 적용된 class는 없으며, css파일로 적용되어있습니다.

- tr : c-week-template / c-week-1(주 차 번호) 로 적용되어있으며, weekTemplate: function 내에서 수정 가능합니다. 적용된 class는 없으며, css파일로 적용되어있습니다.

- td: c-weekday-1(요일번호 0~6) / c-date-1(일자) 로 적용되어 있으며, dayTemplate: function 내에서 수정 가능합니다.

- td: span :: num / today_num (오늘 표시) 로 적용되어 있으며, dayTemplate: function 내에서 수정 가능합니다. 
(span이 아닌 다른 태그로도 custom이 가능합니다!)

- td: basicTemplate :: 기초적으로 설정된 span 태그 다음에 setBasicTemplate: function 으로 설정된 기본 일별 템플릿이 들어갑니다. (존재하지 않는 일자는 건너뜁니다!)

---
## 사용방법

### 1. var tbCalendar = new tableCalendar(); 
클래스를 선언하여 객체에 담습니다.
### 2. tbCalendar.setBasicTemplate(“”);  
일별에 들어갈 기본 템플릿을 설정합니다.
### 3. tbCalendar.init(new Date());
파라미터로 넘긴 Date값으로 클래스의 초기값을 설정해줍니다. !!! renderCalendar:function 을 사용하기 전에 필수적으로 init:function을 호출하여 초기화 하여야 합니다.
### 4. tbCalendar.renderCalendar(tag);
querySelector로 검색가능한 태그의 id나 class값을 파라미터로 넘겨줍니다.
### option: 5. tbCalendar.moveMonth(1);
넘어온 파라미터의 숫자값을 바탕으로 월을 이동하여 init: function을 자동으로 실행해줍니다.
이후에 renderCalendar: function만 호출하면 이동한 달의 템플릿을 그립니다.

* renderCalendar를 추가 호출하도록 개발한 의도는 날짜를 설정하고, getTargetDate: function으로 설정된 날짜값을 통해 템플릿에 원하는 데이터를 그리기 쉽게 하기 위함입니다.

#### moveMonth: function 을 호출할 parameter값 설명
- 0을 넘기면 현재월로 값을 설정합니다.
- 음수는 이전달로 이동합니다. -1 : 한달전, -2: 두달전, -3: 세달전
- 양수는 다음달로 이동합니다. 1: 한달후 …
- 0을 제회한 양, 음수 파라미터는 현재 init: function으로 설정된 날짜값을 기준으로 합니다.
- 현재 init:function 으로 설정된 날짜값을 확인하려면 getTargetDate: function을 호출하세요.

---
