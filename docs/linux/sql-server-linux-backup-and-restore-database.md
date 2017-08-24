---
title: "备份和还原在 Linux 上的 SQL Server 数据库 |Microsoft 文档"
description: "了解如何备份和还原在 Linux 上的 SQL Server 数据库。"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: d30090fb-889f-466e-b793-5f284fccc4e6
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 6bd05a89f0c06bc03de931b898be18f3cbea0c8c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="backup-and-restore-sql-server-databases-on-linux"></a>备份和还原 Linux 上的 SQL Server 数据库

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

使用相同的工具，作为其他平台，可能需要在 Linux 上的 SQL Server 自 2017 年 1 RC2 的数据库的备份。 在 Linux 服务器上，你可以使用`sqlcmd`连接到 SQL Server 并进行备份。 如果是 Windows，则可以在连接到 Linux 上的 SQL Server 后通过用户界面进行备份。 备份功能是相同的跨平台。 例如，你可以备份数据库，本地、 到远程驱动器或[Microsoft Azure Blob 存储服务](http://msdn.microsoft.com/library/dn435916.aspx)。 

## <a name="backup-with-sqlcmd"></a>使用 sqlcmd 备份

在下面的示例`sqlcmd`连接到本地 SQL Server 实例，并采用完整备份的名为的用户数据库`demodb`。

```bash
sqlcmd -H localhost -U SA -Q "BACKUP DATABASE [demodb] TO DISK = N'var/opt/mssql/data/demodb.bak' WITH NOFORMAT, NOINIT, NAME = 'demodb-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
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

### <a name="backup-log-with-sqlcmd"></a>使用 sqlcmd 备份日志

在下面的示例中，`sqlcmd`连接到本地 SQL Server 实例，并采用结尾日志备份。 完成结尾日志备份后，数据库将处于“正在还原”状态。 

```bash
sqlcmd -H localhost -U SA -Q "BACKUP LOG [demodb] TO  DISK = N'var/opt/mssql/data/demodb_LogBackup_2016-11-14_18-09-53.bak' WITH NOFORMAT, NOINIT,  NAME = N'demodb_LogBackup_2016-11-14_18-09-53', NOSKIP, NOREWIND, NOUNLOAD,  NORECOVERY ,  STATS = 5"
```


## <a name="restore-with-sqlcmd"></a>使用 sqlcmd 还原

在下面的示例`sqlcmd`连接到 SQL Server 的本地实例，并将数据库还原。

```bash
sqlcmd -H localhost -U SA -Q "RESTORE DATABASE [demodb] FROM  DISK = N'var/opt/mssql/data/demodb.bak' WITH  FILE = 1,  NOUNLOAD,  REPLACE,  STATS = 5"
```

## <a name="backup-and-restore-with-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS) 备份和还原

从 Windows 计算机中，可以使用 SSMS 连接到 Linux 数据库并执行通过用户界面备份。 

>[!NOTE] 
> 使用最新版本 SSMS 连接到 SQL Server。 若要下载并安装最新版本，请参阅[下载 SSMS](http://msdn.microsoft.com/library/mt238290.aspx)。 

下列步骤将引导通过 SSMS 完成备份。 

1. 启动 SSMS 并连接到 Linux 上的 SQL Server 自 2017 年 1 RC2 中的服务器。

1. 在对象资源管理器，右键单击你的数据库，单击**任务**，然后单击**备份...**.

1. 在**数据库备份**对话框中，验证参数和选项，然后单击**确定**。
 
SQL Server 将完成数据库备份。

有关详细信息，请参阅[使用 SSMS 管理 SQL Server on Linux](sql-server-linux-manage-ssms.md)。

### <a name="restore-with-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS) 还原 

以下步骤将引导使用 SSMS 完成数据库还原。

1. 在 SSMS 中右键单击**数据库**单击**还原数据库...**. 

1. 下**源**单击**设备：** ，然后单击省略号 （…）。

1. 找到你的数据库备份文件并单击**确定**。 

1. 下**还原计划**，验证备份文件和设置。 单击 **“确定”**。 

1. SQL Server 将还原数据库。 

## <a name="see-also"></a>另请参阅

* [创建完整数据库备份 (SQL Server)](http://msdn.microsoft.com/library/ms187510.aspx)
* [备份事务日志 (SQL Server)](http://msdn.microsoft.com/library/ms179478.aspx)
* [BACKUP (Transact-SQL)](http://msdn.microsoft.com/library/ms186865.aspx)
* [SQL Server 备份到 URL](http://msdn.microsoft.com/library/dn435916.aspx)

