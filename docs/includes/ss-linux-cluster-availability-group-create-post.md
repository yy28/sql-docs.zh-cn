---
ms.openlocfilehash: 0cdc343bf4ea6866d1a55672187451a3b6d95ec1
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "68215577"
---

## <a name="add-a-database-to-the-availability-group"></a>将数据库添加到可用性组

确保添加到可用性组的数据库处于完全恢复模式，并具有有效的日志备份。 如果是测试数据库或新建的数据库，请执行数据库备份。 在主 SQL Server 上，运行以下 Transact-SQL 脚本，创建名为 `db1` 的数据库并进行备份：

```sql
CREATE DATABASE [db1];
ALTER DATABASE [db1] SET RECOVERY FULL;
BACKUP DATABASE [db1] 
   TO DISK = N'/var/opt/mssql/data/db1.bak';
```

在主 SQL Server 副本上，运行以下 Transact-SQL 脚本，将名为 `db1` 的数据库添加到名为 `ag1` 的可用性组：

```sql
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];
```

### <a name="verify-that-the-database-is-created-on-the-secondary-servers"></a>验证是否已在辅助服务器上创建了数据库

在每个次要 SQL Server 副本上，运行以下查询，查看是否已创建并同步 `db1` 数据库：

```sql
SELECT * FROM sys.databases WHERE name = 'db1';
GO
SELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;
```
