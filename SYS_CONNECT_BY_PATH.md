- 테이블 생성 
```
CREATE TABLE RecursionTest
(
  id INTEGER NOT NULL,
  name VARCHAR(128) NULL,
  parent INTEGER NULL,
  CONSTRAINT pk_RecursionTest PRIMARY KEY (id)
);
``` 
 
- 테이블 테스트 데이터 입력 
``` 
INSERT INTO RecursionTest (id, name, parent) VALUES (1, 'Root', NULL);
INSERT INTO RecursionTest (id, name, parent) VALUES (2, 'Branch A', 1);
INSERT INTO RecursionTest (id, name, parent) VALUES (3, 'Branch B', 1);
INSERT INTO RecursionTest (id, name, parent) VALUES (4, 'Branch C', 1);
INSERT INTO RecursionTest (id, name, parent) VALUES (5, 'Branch A2', 2);
INSERT INTO RecursionTest (id, name, parent) VALUES (6, 'Branch B2', 3);
INSERT INTO RecursionTest (id, name, parent) VALUES (7, 'Branch B3', 6);
INSERT INTO RecursionTest (id, name, parent) VALUES (8, 'Branch B4', 7);
```

- 계층형 쿼리(SYS_CONNECT_BY_PATH)
```
with recursive cte (clevel, id, name, parent,  id_path) as
(
 select     
 				1 clevel,
 				id,
            name,
            parent,
            cast(id AS CHAR(300) character set utf8) id_path
            #cast(id as char(100) character set utf8) id_path
 from       recursiontest
 where      parent = 1
 union all
 select     
 				cte.clevel + 1,
 				r.id,
            r.name,
            r.parent,
            concat(cte.id_path, '->', r.id) id_path
 from       recursiontest r
 inner join cte
         on r.parent = cte.id
)
 
select * from cte;
```
