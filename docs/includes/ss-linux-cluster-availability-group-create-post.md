
## <a name="add-a-database-to-the-availability-group"></a>将数据库添加到可用性组

确保你将添加到可用性组的数据库处于完整恢复模式，并且具有有效的日志备份。 如果这是一个测试数据库或新创建的数据库，执行数据库备份。 在主 SQL 服务器上，运行下面的 TRANSACT-SQL 脚本，以创建并备份数据库调用`db1`:

```sql
CREATE DATABASE [db1];
ALTER DATABASE [db1] SET RECOVERY FULL;
BACKUP DATABASE [db1] 
   TO DISK = N'/var/opt/mssql/data/db1.bak';
```

在主 SQL Server 副本，运行下面的 TRANSACT-SQL 脚本，以添加一个名为数据库`db1`到可用性组调用`ag1`:

```sql
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];
```

### <a name="verify-that-the-database-is-created-on-the-secondary-servers"></a>验证是否已在辅助服务器上创建了数据库

在每个辅助 SQL Server 副本上，运行以下查询以查看是否`db1`创建和同步数据库：

```sql
SELECT * FROM sys.databases WHERE name = 'db1';
GO
SELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;
```
