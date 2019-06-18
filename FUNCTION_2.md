
- 마리아 DB 오라클 모드로 실행 했을 때 함수 
- MariaDB ( ver. > 10.3 ) 오라클 모드 실행
```
SET SQL_MODE='ORACLE';
```

- DELIMITER(DELIMITER /)로 구분 하고 원래대로 다시 복원(DELIMITER ;)
- BEGIN ~ END 들여쓰기 맞춰야 되는 듯(?)
```
DELIMITER /

CREATE OR REPLACE FUNCTION func_code(param_id VARCHAR) RETURN VARCHAR2 DETERMINISTIC AS
BEGIN
  DECLARE
    vString VARCHAR2(255) := NULL;
  BEGIN
    SELECT name INTO vString FROM TB WHERE id = param_id;
    RETURN vString;
  END;
END func_code;
/

DELIMITER ;
```

- FUNCTION 실행
```
select func_code(2) from dual;
```

- FUNCTION 확인
```
show function status where db='test'
```

참조 사이트 : https://www.fromdual.com/select-hello-world-fromdual-with-mariadb-pl-sql
