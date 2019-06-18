
- MariaDB ( ver. > 10.3 ) 오라클 모드 실행
```
SET SQL_MODE='ORACLE';
```

- 함수 생성 
```
DELIMITER $$
CREATE FUNCTION func3(s VARCHAR)
 RETURN VARCHAR
 IS
 BEGIN
  	RETURN CONCAT('Hello, ',s,'!');
 END; $$
DELIMITER ;
```

- 함수 실행
```
select hello('T') from dual 
```
- 함수 리스트 확인 
```
show function status where db='test'
```
