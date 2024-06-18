## nginx2 sql_file

```sql
#nginx服务器192.168.222.136
#创建数据库
create database if not exists logs;
use logs;

#创建表，设置自增主键，约束时间不重复
create table if not exists log2(
	id int AUTO_INCREMENT PRIMARY KEY，
	time datetime UNIQUE,
	qps int,
	status_200_count int,
	status_500_count int
	);
	
#load data infile 命令导入shell脚本分析好的内容	
load data infile '/var/lib/mysql-files/nginx.logs'
	into table log2
	fields terminated by '/'
	lines terminated by '\n'
	ignore 1 rows
	(
	@time,
	qps,
	status_200_count,
	status_500_count
	)
set time = st'r_to_date(@time, '%Y-%m-%d %H:%i');

#展示导入结果
select * from log2;
```



