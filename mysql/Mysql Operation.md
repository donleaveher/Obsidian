```bash
mysql.server start
```

To start the newly upgraded MySQL server installed via Homebrew, use the command Homebrew provided:
```bash
brew services restart mysql

/opt/homebrew/opt/mysql/bin/mysqld_safe --datadir=/opt/homebrew/var/mysql
```

# Open Mysql
```bash
mysql -u root -p
using user root to open with password
```

# Some basic operation
```bash
show databases;

// switch to dirc
use "database name";
// show the table
show tables;
// select the data
select * from "the target name"
```

# Using Navicat to connect (Connect with GUI tool)
- Connection
- Create the name 
- setting the host, port, User name, and password
- Testing connection

# Download Mysql Shell
```bash
brew install --cask mysql-shell
// Open mysql shell
mysqlsh
```

# Basic Operation
```bash
\help
\connect root@localhost

Switch the language
\py
\sql
\js

Using the database
\use 'database name'
```
🔑 Connect 命令的输入依据
connect 命令遵循一个标准的 URI 格式或简写格式来指定连接参数。其基本结构是：
$$\text{User@Host:Port/Schema}$$
对于你的输入 connect root@localhost，它是最常见的简写格式，其输入依据可以分解为以下三点：
 👥 用户名 (User)
**输入内容：** root
     **依据：** 你想要以 **哪个数据库用户的身份** 连接到 MySQL 服务器。`root` 是 MySQL 服务器上的默认管理用户，拥有最高权限。
    
 🖥️ 主机名 (Host)
**输入内容：** `localhost`
     **依据：** MySQL 服务器 **运行在哪个网络位置**。`localhost` 是一个特殊的保留名称，表示服务器运行在**当前你正在使用命令的这台机器上**。如果服务器在另一台机器上，你需要输入它的 IP 地址或网络主机名（例如：`192.168.1.100` 或 `db.mycompany.com`）。

🔐 认证方式 (Authentication)
**输入内容：** **未显式输入**
    **依据：** 当你输入这个命令后，MySQL Shell 会提示你输入该用户的**密码**，或者根据你的配置文件使用密钥或其他认证方式。

***SQL***
-  DDL: Data Defination Language
	- CREATE | DROP | ALTER | TRUNCATE 
-  DML: Data Manipulation Language
	- INSERT | UPDATE | DELETE | CALL
-  DQL: Data Query Language
	- SELECT
-  DCL: Data Control Language
	- GRANT | REVOKE

```sql
Create and Drop database

create database 'name';
drop database 'name';

show databases; 
// 进入库 
use mydb; 
// 查看库里面的表 
show tables; 
// 查看库的编码，有的编码写中文会报错，这个要注意 
show create database mydb; 
// 删除数据库 
drop database mydb; 
// 修改库的编码 
alter database mydb character set utf8;

CREATE TABLE player(
	id INT,
	name VARCHAR(100),
	level int,
	exp int,
	gold DECIMAL(10,2)
);
DESC player;

ALTER table player MODIFY COLUMN name VARCHAR(200)
ALTER table player RENAME COLUMN name to nick_name
ALTER table player ADD COLUMN last_login DATETIME
ALTER TABLE player DROP COLUMN last_login
DROP TABLE player

ALTER TABLE player DROP COLUMN last_login

INSERT INTO player(id, name, level, exp, gold) VALUES (1, "Nihao", 1, 1, 2);
SELECT * from player
INSERT INTO player(id, name, level, exp, gold) VALUES (2, "Nihao", 2, 1, 2), (3, "Nihao", 4, 1, 2);
ALTER table player MODIFY COLUMN LEVEL INT DEFAULT 1
INSERT INTO player(id, name) VALUES (4, "Nihao");
UPDATE player set level = 10 where id = 4 AND name = "Nihao";

UPDATE player set exp = 0, gold =0

DELETE from player where id = 1;
```

# Export and Import the data
```sql
mysqldump -u root -p --set-gtid-purged=OFF --single-transaction 数据库名 > backup.sql

mysql -u root -p game < game.sql
```

# Selection
```sql
SELECT * FROM player WHERE level > 1 and level < 6 or exp < 5
SELECT * from player WHERE level in (1,2,3,4,5)
SELECT * FROM player WHERE level BETWEEN 1 AND 10
SELECT * from player WHERE level NOT in (1,2,3,4,5)
SELECT * FROM player WHERE name LIKE '%王%'
SELECT * FROM player WHERE name LIKE '王%'
SELECT * FROM player WHERE name LIKE '王_'

Regular expression

SELECT * From player where name REGEXP '^王.$'
SELECT * From player where name REGEXP '王'
SELECT * From player where name REGEXP '王|张'
SELECT * From player where name REGEXP '[王张]'

Exercise

SELECT * FROM player where email REGEXP '^zhangsan'
SELECT * FROM player where email like 'zhangsan%'
SELECT * FROM player where email REGEXP '^[abc]'
SELECT * FROM player where email REGEXP '^[a-d]'
SELECT * FROM player where email REGEXP 'net$'
SELECT * FROM player where email like '%net'

```

# Basic Select & Filter
```sql
-- 查找 email 为 NULL（未填）或者 为空字符串（填了但没内容）的玩家
SELECT * FROM player where email is null or email = '';

-- 多重排序：先按 level 从大到小(DESC)排；如果 level 相同，再按 exp 从小到大(默认ASC)排
SELECT * FROM player ORDER BY level DESC, exp;

-- 按第 5 列排序（不推荐写法，数字代表 select 中的第几列，代码可读性差）
SELECT * FROM player ORDER BY 5;

-- 统计 player 表里总共有多少行数据
SELECT COUNT(*) FROM player;

-- 计算所有玩家 level 的平均值
SELECT AVG(level) FROM player;
```

# Grouping & Aggregation
```sql
-- 按性别分组，计算每种性别各有多少人
SELECT sex, count(*) from player GROUP BY sex; 

-- 分组后筛选 (HAVING)：
-- 1. 按等级分组
-- 2. 统计每个等级有多少人
-- 3. 筛选出人数大于 4 的等级
-- 4. 最后按等级降序排列
SELECT level, count(level) from player 
GROUP BY level 
having count(level)>4 
ORDER BY level DESC;

-- 复杂的字符串处理与分组：
-- 1. SUBSTR(name,1,1): 截取名字的第一个字符（比如 'Amy' 截取 'A'）
-- 2. 统计每个首字母出现的次数
-- 3. HAVING: 只保留出现次数大于 2 的首字母
-- 4. ORDER BY: 按出现次数从多到少排序
-- 5. LIMIT 3, 6: 分页。跳过前 3 条，取接下来的 6 条数据
SELECT SUBSTR(name,1,1), COUNT(SUBSTR(name,1,1)) from player 
GROUP BY SUBSTR(name,1,1) 
having COUNT(SUBSTR(name, 1, 1))>2 
ORDER BY COUNT(SUBSTR(name,1,1)) DESC
LIMIT 3, 6;

-- 去重：查看表里有哪些不同的性别（不显示重复的）
SELECT DISTINCT sex from player;
```

# Set Operation
```sql
-- UNION (并集): 
-- 找出等级 1-10 的人，或者是经验 1-5 的人。
-- 两个结果拼在一起，会自动去重。
SELECT * FROM player WHERE level BETWEEN 1 AND 10
UNION
SELECT * from player WHERE exp in (1,2,3,4,5);

-- INTERSECT (交集 - MySQL 8.0.31+ 才支持):
-- 找出等级是 1-10，并且经验也是 1-5 的人（同时满足两个条件）。
SELECT * FROM player WHERE level BETWEEN 1 AND 10
INTERSECT
SELECT * from player WHERE exp in (1,2,3,4,5);
```

# Subqueries
```sql
-- CTAS (Create Table As Select):
-- 创建一张新表叫 news，并将 player 表里 level < 5 的数据直接复制过去（包括表结构和数据）。
CREATE table news SELECT * FROM player WHERE level < 5;

-- 查看新表的数据
SELECT * from news;

-- 将查询结果插入已存在的表中:
-- 把 player 表里 level 在 3 到 10 之间的数据，追加插入到 news 表里。
INSERT into news SELECT * FROM player where level BETWEEN 3 and 10;
```

# Table Operation
```sql
-- CTAS (Create Table As Select):
-- 创建一张新表叫 news，并将 player 表里 level < 5 的数据直接复制过去（包括表结构和数据）。
CREATE table news SELECT * FROM player WHERE level < 5;

-- 查看新表的数据
SELECT * from news;

-- 将查询结果插入已存在的表中:
-- 把 player 表里 level 在 3 到 10 之间的数据，追加插入到 news 表里。
INSERT into news SELECT * FROM player where level BETWEEN 3 and 10;
```

# Joins
```sql
-- 仅仅是列出关键字，实际使用需要配合 ON 条件
INNER JOIN -- 内连接：两边都有才保留
LEFT JOIN  -- 左连接：保留左表所有行
RIGHT JOIN -- 右连接：保留右表所有行

-- 查看 equip 表的结构 (Describe)
DESC equip;

-- 右连接示例:
-- 保留 equip (右表) 的所有数据。
-- 如果 equip 里有某个 player_id 在 player (左表) 里找不到，左表字段显示 NULL。
SELECT * from player
RIGHT JOIN equip
on player.id = equip.player_id;
```

# Index & Performance
```sql
-- 查看 fast 表结构
DESC fast;

-- 统计 fast 表行数
SELECT count(*) from fast;

-- 创建索引:
-- 在 fast 表的 column_name 列上建立名为 email_index 的索引。
-- 注意：你代码里写的 on fast(index) 里的 index 可能是笔误，应该是字段名，比如 fast(email)。
CREATE index email_index on fast(email); 

-- 查看 fast 表目前有哪些索引
show index from fast;

-- 性能对比测试：
-- 在 slow 表（假设无索引）查找 'abcd' 开头的 email
SELECT * from slow where email like 'abcd%' ORDER BY id;
-- 在 fast 表（有索引）查找同样的数据（理论上速度极快）
SELECT * from fast where email like 'abcd%' ORDER BY id;

-- 删除索引：删除 fast 表上名为 email_index 的索引
drop index email_index on fast;

-- 添加索引的另一种写法 (ALTER TABLE)：
-- 给 fast 表的 name 字段添加一个名为 name_index 的索引
ALTER table fast add index name_index(name);
```

# Views
```sql
-- 创建视图 (虚拟表):
-- 创建一个叫 top20 的视图，里面永远存着等级最高的 20 个人。
CREATE VIEW top20
AS
SELECT * from player order by level desc LIMIT 20;

-- 像查普通表一样查视图
SELECT * from top20;

-- 修改视图定义:
-- 把 top20 改为只取前 20 个（不再按 level desc 排序，变成默认排序）。
ALTER VIEW top20
AS
SELECT * from player ORDER BY level LIMIT 20;

-- 删除视图
drop view top10; -- 注意：上面你创建的是 top20，这里删的是 top10，名字要对应。
```