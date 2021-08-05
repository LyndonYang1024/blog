1. 安装目录各个目录介绍

   1.1 base：包含数据库用户所创建的各个数据库

   1.2 global：包含集群范围的各个表，这里有很多表以及视图来跟踪整个集群

   1.3 pg_clog：包含事务提交状态数据

   1.4 pg_multixact：包含多事务状态数据（等待锁定的并发事务）

   1.5 pg_serial：包含已提交的序列化事务的有关信息

   1.6 pg_stat_tmp：包含统计子系统的临时文件

   1.7 pg_subtrans：包含子事务状态数据

   1.8 pg_tblspc：包含表空间的符号链接

   1.9 pg_twophase：包含预备事务的状态文件

   1.10 pg_xlog：包含预写日志文件

2. psql中执行**\dx**命令可以查看已经安装的contrib插件情况，查询视图**pg_available_extensions**可以列出所有可用插件

   安装删除插件使用如下命令：

   ```sql
   create extension dblink;
   drop extension dblink;
   ```

3. **pg_relation_filepath**可以查看表的数据文件路径

4. **保存点（savepoint）：**当一个事务中出现错误的时候，可以返回到savepoint的位置

   ```sql
   postgres=# begin;
   BEGIN
   postgres=*# select count(*) from t;
    count
   -------
        0
   (1 row)
   
   postgres=*# savepoint a;
   SAVEPOINT
   postgres=*# select 2 / 0;
   ERROR:  division by zero
   postgres=!# rollback to sav
   
   postgres=!# rollback to save
   
   postgres=!# rollback to savepoint a;
   ROLLBACK
   postgres=*# select 3;
    ?column?
   ----------
           3
   (1 row)
   
   postgres=*# commit;
   COMMIT
   ```

   

5. 