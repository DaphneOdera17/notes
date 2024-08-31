启动 neo4j 
```shell
neo4j.bat console
```
http://localhost:7474/browser/

用户名 neo4j
密码 12345678
## 查看所有节点
```Cypher
MATCH (n) RETURN n
```
## 删除所有节点
```Cypher
MATCH (n) DETACH DELETE n;
```
## 添加节点
```Cypher
CREATE (a:Person {name: 'Alice', age: '25'})
CREATE (b:Person {name: 'Bob', age: '30'})
CREATE (c:Person {name: 'Charlie', age: '35'})
CREATE (a)-[:FRIENDS]->(b)
CREATE (b)-[:FAMILY]->(c)
```

```Cypher
CREATE (d:Person {name: 'David', age: 28});
CREATE (e:Person {name: 'Eve', age: 22});
CREATE (f:Person {name: 'Frank', age: 31});

MATCH (d:Person {name: 'David'}), (e:Person {name: 'Eve'})
CREATE (d)-[:COLLEAGUES]->(e);

MATCH (e:Person {name: 'Eve'}), (f:Person {name: 'Frank'})
CREATE (e)-[:FRIENDS]->(f);
```

## 修改密码
网页输入框
```neo4j
:server change-password
```