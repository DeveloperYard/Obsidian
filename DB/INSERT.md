
> 데이터베이스 객체에 데이터를 입력하는 SQL 문

```MySQL

-- 컬럼의 순서와 개수를 반드시 맞춰줘야 함!
INSERT INTO table_name VALUES (col_val1, col_val2, ..., col_valN);


-- 컬럼에 해당하는 값을 매핑해주면 됨!, 가능하면 명시를 해주는 것이 좋음!
INSERT INTO table_name (col_name1, col_name2, ..., col_nameN) VALUES (col_val1, col_val2, ..., col_valN);

-- *** 생략이 가능한 필드 ***
-- 1. NULL이 허용된 컬럼, NOT NULL이면 생략 절대로 안됨!!
-- 2. DEFAULT가 설정된 컬럼
-- 3. AUTO INCREMENT가 설정된 컬럼

-- 하나의 테이블에다가 한 번에 여러 개의 행을 insert할 수 있음!
-- 하나의 쿼리문으로 여러 개를 생성할 수 있으므로 더 효율적이다.
INSERT INTO table_name (col_name1, col_name2, ..., col_nameN) VALUES (col_val1, col_val2, ..., col_valN),
		(col_val1, col_val2, ..., col_valN);


-- 하나의 Query문 실행 과정
-- 1. Driver Loading
-- 2. DB 연결
-- 3. SQL 실행 준비
-- 4. SQL 문장 실행
-- 5. DB 연결 해제
```

> VM이 판단할 수 있는 시간 -> 1/10억 초, DB연결은 우리가 볼 수 있을 정도로 느림. 따라서 한 번에 처리하는 게 훨씬 효율적임!



- auto_increment : 넣지 않으면 자동으로 증가함!
- default : 값을 넣지 않으면 뒤에 것을 넣음!
```MySQL
    -- ex) timestamp에 값이 들어오지 않으면 current_timestamp()로 설정하겠다는 뜻임!
    
    joindate timestamp		default		current_timestamp(),
```


#### NOT NULL인 곳에 값을 할당하지 않았을 때 발생하는 에러

```shell
Error Code: 1364. Field 'userid' doesn't have a default value
```


### Q. 
- Auto_increment 쓸거면 not null이 필요 없는게 아닌가?
- values와 value의 차이? 어제 썼던 것 같은데..


## cf

- now(), current_timestamp() : select문의 실행 시간
- sysdate() : 함수가 호출될 때의 시간, 즉 셋이 같이 쓰게 되면 가장 나중에 실행된 시간이 출력된다.

```MySQL
select now(), sleep(3), current_timestamp(), sleep(3), sysdate();
-- 결과 : now(), current_timestamp() 먼저 출력 후 6초 뒤에 sysdate() 출력
```

- ==table 잘못 만들어지면 drop으로 날리고 다시 create 하는걸로 ㅋㅎㅋㅎㅋ==

