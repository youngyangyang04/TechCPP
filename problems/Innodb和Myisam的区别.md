数据库引擎是用于存储、处理和保护数据的核心服务

1.事务

InnoDB 支持事务，事务安全。Myisam 非事务安全，也不支持事务

2.锁

innoDb 行级锁，myisam 针对表加锁

3.索引

innodb 不支持全文索引，myisam 支持全局索引

4.适用场景

myisam 效率快于 innodb ，适用于小型应用，扩平台支持。大量查询 select

innodb 支持事务，也有 ACID 的特性还有 insert update 对于事务的控制操作