> Table에 있는 것을 변경하는 SQL 문

``` MySQL
UPDATE table_name
	SET col_name1 = col_val1, [col_name2 = col_val2, ..., 
		col_nameN = col_valN]
	WHERE conditions;

-- WHERE절의 조건에 만족하는 레코드의 값을 변경
```
#### ==주의 : WHERE 절을 생략하면 모든 데이터가 변경된다!==


