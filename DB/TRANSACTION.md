
## Content

1. [JDBC INSERT Query](#INSERT QUERY)
2. [JDBC UPDATE Query](#UPDATE QUERY)
3. [JDBC DELETE Query](#DELETE QUERY)

---

> 데이터베이스의 상태를 변화시키는 일종의 작업 단위를 의미한다.

![[Pasted image 20230913095636.png]]

-> 표 만들기!

> 적용 시키는 것은 Commit, 날리는 것은 rollback!

완전히 커밋되기 전까지는 메모리 공간에 저장됨

> Auto commit 은 쿼리문이 생성될 때마다 자동 커밋이 되므로 롤백이 의미가 없을 수 있음, 항상 조심!!!

### Rollback
```MySQL
create table tc_test
(
	val varchar(10)
);

start transaction;

insert into tc_test
values ('a');

insert into tc_test
values ('b');

insert into tc_test
values ('c');

select * from tc_test;
-- a, b, c 3개의 행이 출력됨, 그러나 실제 파일에 저장된 것은 아님!

rollback;
-- 마지막 커밋 직후로 되돌림!

select * from tc_test;
-- 아무것도 출력하지 않음 -> 트랜잭션 후 롤백하면 저장되지 않는다는 것을 의미.
```


### Commit
```MySQL
start transaction;

insert into tc_test
values ('a');

insert into tc_test
values ('b');

insert into tc_test
values ('c');

commit;
-- 여기서 데이터베이스에 반영됨

select * from tc_test; 
-- a, b, c 3개의 행이 출력됨

rollback;
-- 커밋된 직후로 갔지만, 이미 저장된 이후이므로 출력하면 3개가 모두 출력됨.

select * from tc_test; 
-- a, b, c 3개의 행이 출력됨
```


### DELETE & TRUNCATE

> DELETE는 DATA가 롤백이 되지만, TRUNCATE는 롤백이 되지 않음!

```MySQL
delete tc_test;
truncate tc_test;
```


## save point

> 트랜잭션 중에 깃발 하나를 꽂아 두는 것 즉, 그 때 까지의 트랜잭션 결과를 기억함

```MySQL
start transaction;

insert into tc_test
values ('a');

insert into tc_test
values ('b');

insert into tc_test
values ('c');

savepoint f1;

insert into tc_test
values ('d');

insert into tc_test
values ('e');

insert into tc_test
values ('f');

select *
from tc_test;
-- a, b, c, d, e, f 모두 출력

rollback to f1;
-- f1 savepoint까지만 롤백!

select *
from tc_test;
-- a, b, c 출력
```


## [[INSERT QUERY]]
## [[UPDATE QUERY]]
## [[DELETE QUERY]]
