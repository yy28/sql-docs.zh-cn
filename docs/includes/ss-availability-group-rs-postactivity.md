
## <a name="add-a-database-to-the-availability-group"></a>将数据库添加到可用性组

确保添加到可用性组的数据库处于完全恢复模式，并具有有效的日志备份。 如果数据库是测试数据库或新建的数据库，请执行数据库备份。 若要创建和备份名为 `db1` 的数据库，请在主 SQL Server 实例上运行以下 Transact-SQL 脚本：

```sql
CREATE DATABASE [db1];
ALTER DATABASE [db1] SET RECOVERY FULL;
BACKUP DATABASE [db1]
   TO DISK = N'/var/opt/mssql/data/db1.bak';
```

若要将名为 `db1` 的数据库添加到名为 `ag1` 的可用性组中，请在主 SQL Server 副本上运行以下 Transact-SQL 脚本：

```sql
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];
```

### <a name="verify-that-the-database-is-created-on-the-secondary-servers"></a>验证是否已在辅助服务器上创建了数据库

若要查看是否创建并同步了 `db1` 数据库，请在每个次要 SQL Server 副本上运行以下查询：

```sql
SELECT * FROM sys.databases WHERE name = 'db1';
GO
SELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;
```
