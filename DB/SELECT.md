> ==select, from은 항상 같이 쓰자!==

```mySQL
select now();
from dual;
```
현재 시간을 나타내는 select 명령문

- dual이 뭘까?

```MySQL
select employee_id, first_name, 
	salary, salary*12 as yearSalary,  
    commission_pct, salary * (1 + ifnull(commission_pct, 0)) as salaryPlusYearSalary
from employees;
```

-> 이와 같이 Alias 사용 가능

- ifnull(검증할 값, null일 시 초기화할 값)

### CASE

CASE ~ WHEN 형식으로 사용

```MySQL
-- 모든 사원의 사번, 이름, 급여, 급여에 따른 등급표시 검색.
-- 급여에 따른 등급
 --  15000 이상 “고액연봉“      
--   8000 이상 “평균연봉”      
--   8000 미만 “저액연봉＂
select employee_id, first_name, salary,
	case 
		when salary >= 15000 then "highPaid"
		when salary >= 8000 then "midPaid"
        else "lowPaid"
	end "연봉등급"
from employees;
```

이와 같이 사용할 수 있고, when ~ then 절을 모두 사용한 후 나머지 조건엔 else, case 문을 끝내고 싶다면 end 적어주기!

## ==WHERE==

```MySQL
-- 부서번호가 50인 사원중 급여가 7000이상인 사원의
-- 사번, 이름, 급여, 부서번호
select employee_id, first_name, salary, department_id
from employees
where department_id=50 and salary >= 7000;
```

이렇게 직접적으로 Where절에 and 혹은 or를 사용할 수 있음!

```MySQL
-- 근무 부서번호가 50, 60, 70에 근무하는 사원의 사번, 이름, 부서번호
select employee_id, first_name, department_id
from employees
where department_id = 50 or department_id = 60 or department_id = 70
order by department_id asc;
```

order by 후 정렬할 기준 값 대입, asc(오름차순)가 기본값이고, desc(내림차순)을 지정하여 할 수 있다.

```MySQL
-- 근무 부서번호가 50, 60, 70이 아닌 사원의 사번, 이름, 부서번호
select employee_id, first_name, department_id
from employees
where department_id != 50 and department_id != 60 and department_id != 70
order by department_id asc;
```

**or이 아닌 and가 와야** 아닌 사람들을 뽑을 수 있음!

```MySQL
select employee_id, first_name, department_id
from employees
where department_id not in (50, 60, 70)
order by department_id asc; 
```

==not in==을 이용하면 더 간단하게 처리 가능

>  두 개 다 null을 포함하지 않는다!


```MySQL
-- 급여가 6000이상 10000이하인 사원의 사번, 이름, 급여
select employee_id, first_name, salary
from employees
where salary between 6000 and 10000;
```

이상, 이하 값을 구할 수 있음! ==between A and B;==


```MySQL
-- 근무 부서가 지정되지 않은(알 수 없는) 사원의 사번, 이름, 부서번호 검색.
select employee_id, first_name, department_id
from employees
where department_id is null;

-- 커미션을 받는 사원의 사번, 이름, 급여, 커미션
select employee_id, first_name, salary, commission_pct
from employees
where commission_pct is not null;
```

-> is null, is not null 활용하여 쿼리 가능!


```MySQL
-- 이름에 'x'가 들어간 사원의 사번, 이름
select employee_id, first_name
from employees
where first_name like '%x%';
```
-> 어디든 들어갈 수 있으므로 '%'를 앞 뒤에 넣어놓음
- '%x'  : 뒤에 x가 들어감
- 'x%'  : 앞에 x가 들어감


```MySQL
-- 이름의 끝에서 3번째 자리에 'x'가 들어간 사원의 사번, 이름
select employee_id, first_name
from employees
where first_name like '%x__';
```
-> 언더바 개수 당 글자 수라고 보면 됨!

### Q) 검색해야 하는 문자열 내에 '%'가 들어가 있는 정보가 있다면, 어떻게 검색해야 할까?



```MySQL
-- 모든 사원의 사번, 이름, 급여
-- 단 급여순 정렬(내림차순)
select employee_id, first_name, salary
from employees
order by salary desc;
```
이와 같이 정렬할 수 있음, ==기본 값은 오름차순!==

```MySQL
-- 50, 60, 70에 근무하는 사원의 사번, 이름, 부서번호, 급여
-- 단, 부서별 정렬(오름차순) 후 급여순(내림차순) 검색
select employee_id, first_name, department_id, salary
from employees
order by department_id asc, salary desc;
```

이와 같이 정렬을 여러 기준을 가지고 할 수 있음!
salary로 전체 데이터를 재정렬하는 것이 아닌 부서 내에서 정렬이 된다는 점을 꼭 알고 있자!

```MySQL
select employee_id, first_name, department_id, salary
from employees
order by 1 desc;
```
이렇게 하면 employee_id 로도 정렬이 가능하지만, 직관적이지 않아 이름을 제대로 써주는게 더 나음!



### cf ) ==null은 equal 비교로 볼 수 없다!== isnull() 등 함수를 사용해야 함!==

### cf) ==null에 not을 붙이면 null이 나옴, NULL에 ==True나 false를 and, or하면 모두 결과는 NULL이 나옴==

