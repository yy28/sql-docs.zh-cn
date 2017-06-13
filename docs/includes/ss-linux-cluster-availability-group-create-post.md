
## <a name="add-a-database-to-the-availability-group"></a>将数据库添加到可用性组

确保要添加到可用性组的数据库处于完全恢复模式，并具有有效的日志备份。 如果是测试数据库或新建的数据库，请执行数据库备份。 在主 SQL 服务器上，运行以下 TRANSACT-SQL 创建和调用将数据库备份`db1`。

```Transact-SQL
CREATE DATABASE [db1];
ALTER DATABASE [db1] SET RECOVERY FULL;
BACKUP DATABASE [db1] 
   TO DISK = N'var/opt/mssql/data/db1.bak';
```

在主 SQL Server 副本上，运行以下 TRANSACT-SQL 将添加一个名为数据库`db1`到可用性组调用`ag1`。

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];
```

### <a name="verify-that-the-database-is-created-on-the-secondary-servers"></a>验证是否已在辅助服务器上创建了数据库

在每个辅助 SQL Server 副本上，运行以下查询以查看是否`db1`数据库已创建，并且已同步。

```Transact-SQL
SELECT * FROM sys.databases WHERE name = 'db1';
GO
SELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;
```
