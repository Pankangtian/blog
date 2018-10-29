---
title: mysql使用指南
date: 2018-10-22 12:12:30
tags: mysql
categories: 笔记
---

### 一、 mysql的yum安装
本文的mysql 安装基于 centos 7 系统，仅供参考
1. 执行安装mysql命令      
       yum install mysql mysql-server mysql-devel -y
 如果安装过程中有选择，选择 是或y即可
2.  启动和关闭mysql  
启动 mysql命令                     
        systemctl start mysqld      (centos 7)
        service mysqld start        （centos 6)
关闭mysql命令        
        systemctl stop mysqld      (centos 7)
        service mysqld stop        （centos 6)
重启mysql  
        systemctl restart mysqld      (centos 7)
        service mysqld restart        （centos 6)
加入开机自启动          
        systemctl enable mysqld      (centos 7)
        service mysqld enable        （centos 6)    

###  二、配置mysql
1. 设置密码     
        mysqladmin -u root password '你的密码'
2. 检查密码设置         
通过mysql -u root -p 命令登陆mysql 查看刚设置的密码是否生效
        mysql -u root -p
3. 忘记密码，后重置密码     
 首先停止sql服务，具体命令查看mysql的yum安装部分    
 其次通过不检查权限形式启动mysql  ,此时mysql可以无密登陆   
           mysqld --skip-grant-tables
登陆mysql，运行sql语句修改root密码
          mysql> UPDATE mysql.user SET Password=PASSWORD('123456')  WHERE User='root';
          mysql> FLUSH PRIVILEGES;   
运行后，重启mysql服务器即可，密码已改为新设置密码。
4. mysql配置文件my.ini 文件详解          
 文件详细配置不再详述，详情可[点击此处](https://www.cnblogs.com/SamWeb/p/7922490.html)     


 ###  三、mysql 语句    
 1.  表的创建  
 必要：   
 每一张表必须拥有主键，主键最好采用int型，而企业级数据较大，采用bigint最好。字段的命名要体现处字段的含义，字段名字不应该太长两到三个单词内最好，命名最好遵循驼峰规则。字段属性应该根据存值的不同采用不同的类型，如果存储固定值的最好存为枚举或直接存为tinyint，字符串可采用varchar，尽量不要使用text blog等。数据库字段必须要有注释，这时一个很好的习惯。对于表的索引一定要酌情建立，不必要的索引坚决不要建立，索引的维护会增加数据库的负担。  
 建议：   
 每一个字段尽量不要存储null，数据库对null值的处理成本相对是比较高的，对于每个字段可相应给于默认值。每一张表可酌情添加create_time 、update_time 字段，并将其值交由数据库自行赋值（可参考面语句），数据尽量不要直接删除，最好使用软删除，即添加删除is_deleted标记字段。表之间可以用外键，但最好还是在应用级实现控制，尽量不要定义外键。
         DROP TABLE
         IF EXISTS `user`;
         CREATE TABLE `USER` (
         	`id` BIGINT PRIMARY KEY AUTO_INCREMENT COMMENT '主键',
         	`name` VARCHAR (20) NOT NULL DEFAULT '' COMMENT '姓名',
         	`sex` enum ('男', '女') NOT NULL DEFAULT '男' COMMENT '男 0 女 1 ',
         	`job_id` INT NOT NULL DEFAULT 0 COMMENT '工作，默认为0 即无职业',
         	`create_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
         	`update_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
         	`is_deleted` TINYINT NOT NULL DEFAULT 0 COMMENT '是否已删除， 0未 ，1 是',
         	INDEX (NAME),         	#  UNIQUE
         	CONSTRAINT user_job FOREIGN KEY (job_id) REFERENCES JOB (id) #on delete cascade
         ) ENGINE = INNODB CHARSET = utf8;

2. 查询
mysql 的基本查询格式如下      
        select 查询内容  
          from 表名
          where 表达式  
          group by 字段名
          having 表达式
          order by 字段名
          limit 记录数                    
简单查询语句有     
        select * from user;  或        select name,age from user;
        select * from user where  age between 5 and 12;  #条件查询
        select * from user where  age > 5 and age< 12;  
        select * from user where age is NOT NULL; #非空查询
        select name from user where name like '11__'; #模糊查询
        select age from user where age not in (14,46); #in  / not in
分组查询   
select 查询内容 from 表名    group by 分组依据 [having表达式条件]  
        select NAME from user group by job_id having age>18;

where 与 having：     
    where 与 having关键字都用于设置条件表达式对查询结果进行过滤，区别是having后面可以跟聚合
    函数，而where不能，通常having关键字都与group by 一起使用，表示对分组后的数据进行过滤    
order by用于排序， 排序条件 asc/desc，asc表示升序 desc表示降序
limit 用于限制 查询 具体返回哪几条记录






 ### 四、 mysql优化建议
