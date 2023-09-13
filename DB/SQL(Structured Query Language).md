- Database에 있는 정보를 사용할 수 있도록 지원하는 언어
- 모든 DBMS에서 사용 가능
- Query의 대소문자는 구분하지 않음(단, **데이터의 대소문자는 구분**)
	- MySQL은 데이터의 대소문자도 구분하지 않음


```mySQL
varchar(20) binary
```

이렇게 하면 binary로 대소문자 구분 가능! 일반적으로는 구분하지 않음.

또 다른 방식으로는 다음과 같다.

```mySQL
-- 함수 이용
select *
from employees
where binary(first_name) = 'Steven';

desc employees;
```


> DB의 파일과 SQL을 연결하기 위해 DBMS가 존재하는 것

### INSERT vs. CREATE

- INSERT : DB에 정보 삽입
- CREATE : 스키마 생성

> Transaction 개념을 알자!

## [[DDL(Data Definition Language)]]

## [[DML(Data Manipulation Language)]]

## [[TRANSACTION]]

## [[DCL(Data Control Language)]]

## [[TCL]]

## [[SET]]

## [[Function]]
