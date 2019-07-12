---
title: 备份和还原 Linux 上的 SQL Server 数据库
description: 了解如何备份和还原 Linux 上的 SQL Server 数据库。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 11/14/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: d30090fb-889f-466e-b793-5f284fccc4e6
ms.openlocfilehash: 4722afd669893dc4bfa9cad23a7c97cdef5cc182
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834205"
---
# <a name="backup-and-restore-sql-server-databases-on-linux"></a>备份和还原 Linux 上的 SQL Server 数据库

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

使用与其他平台相同的工具，可能需要 SQL Server 2017 Linux 上的数据库的备份。 在 Linux 服务器上，可以使用**sqlcmd**连接到 SQL Server 并进行备份。 如果是 Windows，则可以在连接到 Linux 上的 SQL Server 后通过用户界面进行备份。 备份功能是相同的跨平台。 例如，本地、 远程驱动器或备份数据库[Microsoft Azure Blob 存储服务](../relational-databases/backup-restore/sql-server-backup-to-url.md)。

## <a name="backup-a-database"></a>备份数据库

在下面的示例**sqlcmd**连接到本地 SQL Server 实例，并采用完整备份的名为的用户数据库`demodb`。

```bash
sqlcmd -S localhost -U SA -Q "BACKUP DATABASE [demodb] TO DISK = N'/var/opt/mssql/data/demodb.bak' WITH NOFORMAT, NOINIT, NAME = 'demodb-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
```

运行该命令后，SQL Server 将提示输入密码。 输入密码后，shell 将返回备份进度结果。 例如：

```
Password:
10 percent processed.
21 percent processed.
32 percent processed.
40 percent processed.
51 percent processed.
61 percent processed.
72 percent processed.
80 percent processed.
91 percent processed.
Processed 296 pages for database 'demodb', file 'demodb' on file 1.
100 percent processed.
Processed 2 pages for database 'demodb', file 'demodb_log' on file 1.
BACKUP DATABASE successfully processed 298 pages in 0.064 seconds (36.376 MB/sec).
```

### <a name="backup-the-transaction-log"></a>备份事务日志

如果你的数据库处于完整恢复模式，您还可以更精细的还原选项的事务日志备份。 在以下示例中， **sqlcmd**连接到本地 SQL Server 实例，并将事务日志备份。

```bash
sqlcmd -S localhost -U SA -Q "BACKUP LOG [demodb] TO DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak' WITH NOFORMAT, NOINIT, NAME = N'demodb_LogBackup', NOSKIP, NOREWIND, NOUNLOAD, STATS = 5"
```

## <a name="restore-a-database"></a>还原数据库

在下面的示例**sqlcmd**连接到 SQL Server 的本地实例，并将 demodb 数据库还原。 请注意，`NORECOVERY`选项用于允许其他的日志文件备份还原。 如果不打算还原其他日志文件，删除`NORECOVERY`选项。

```bash
sqlcmd -S localhost -U SA -Q "RESTORE DATABASE [demodb] FROM DISK = N'/var/opt/mssql/data/demodb.bak' WITH FILE = 1, NOUNLOAD, REPLACE, NORECOVERY, STATS = 5"
```

> [!TIP]
> 如果你意外地使用 NORECOVERY，但不是具有额外的日志文件备份，运行命令`RESTORE DATABASE demodb`不带任何其他参数。 这完成还原并保持您的数据库操作状态。

### <a name="restore-the-transaction-log"></a>还原事务日志

以下命令将还原以前的事务日志备份。

```bash
sqlcmd -S localhost -U SA -Q "RESTORE LOG demodb FROM DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak'"
```

## <a name="backup-and-restore-with-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS) 备份和还原

可以从 Windows 计算机使用 SSMS 连接到 Linux 数据库并进行备份通过用户界面。

>[!NOTE] 
> 使用最新版本 SSMS 连接到 SQL Server。 若要下载并安装最新版本，请参阅[下载 SSMS](../ssms/download-sql-server-management-studio-ssms.md)。 有关如何使用 SSMS 的详细信息，请参阅[使用 SSMS 管理 Linux 上的 SQL Server](sql-server-linux-manage-ssms.md)。

下列步骤将引导通过 SSMS 完成备份。 

1. 启动 SSMS 并连接到 Linux 上的 SQL Server 2017 中的服务器。

1. 在对象资源管理器，右键单击数据库，单击**任务**，然后单击**备份...** .

1. 在中**数据库备份**对话框中，验证参数和选项，然后单击**确定**。
 
SQL Server 将完成数据库备份。

### <a name="restore-with-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS) 还原 

以下步骤将引导使用 SSMS 完成数据库还原。

1. 在 SSMS 中右键单击**数据库**单击**还原数据库...** . 

1. 下**源**单击**设备：** ，然后单击省略号 （...）。

1. 找到您的数据库备份文件，然后单击**确定**。 

1. 下**还原计划**，验证备份文件和设置。 单击 **“确定”** 。 

1. SQL Server 将还原数据库。 

## <a name="see-also"></a>请参阅

* [创建完整数据库备份 (SQL Server)](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
* [备份事务日志 (SQL Server)](../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)
* [BACKUP (Transact-SQL)](../t-sql/statements/backup-transact-sql.md)
* [SQL Server 备份到 URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)
