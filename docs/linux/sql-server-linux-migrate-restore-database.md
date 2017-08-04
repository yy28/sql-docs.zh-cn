---
title: "从 Windows 的 SQL Server 数据库迁移到 Linux |Microsoft 文档"
description: "本主题演示如何在 Windows 上，执行 SQL Server 数据库备份并将其还原到运行 SQL Server 自 2017 年 1 RC2 的 Linux 计算机。"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 2e23ba46381b1fb80b8ac335f6d7630f02a222bb
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>使用备份和还原将 SQL Server 数据库从 Windows 迁移到 Linux

SQL Server 的备份和还原功能是从在 Windows 上的 SQL Server 的数据库迁移到在 Linux 上的 SQL Server 自 2017 年 1 RC2 的建议的方法。 本主题介绍使用此方法的分步说明。 在本教程中，你将学习：

- 下载 Windows 计算机上的 AdventureWorks 备份文件
- 将备份转移到 Linux 计算机
- 使用 Transact-SQL 命令还原数据库

> [!NOTE] 
> 本教程假定你已安装[SQL Server 自 2017 年 1 RC2](sql-server-linux-setup.md)和[SQL Server 工具](sql-server-linux-setup-tools.md)目标 Linux 服务器上。

## <a name="download-the-adventureworks-database-backup"></a>下载 AdventureWorks 数据库备份

尽管可使用同样的步骤还原任何数据库，但 AdventureWorks 示例数据库提供了一个很好的示例。 它用作现有数据库备份文件。

>[!NOTE] 
> 若要将数据库还原到 Linux 上的 SQL Server，必须从 SQL Server 2014 或 SQL Server 2016 获取源备份。 备份 SQL Server 内部版本号不能超过还原 SQL Server 内部版本号。  

1. 在您的 Windows 计算机，转到[https://msftdbprodsamples.codeplex.com/downloads/get/880661](https://msftdbprodsamples.codeplex.com/downloads/get/880661)并下载**Adventure Works 2014 完整数据库 Backup.zip**。

   > [!TIP] 
   > 本教程演示了如何在 Windows 和 Linux 之间进行备份和还原，但也可以在 Linux 上使用浏览器直接将 AdventureWorks 示例下载到 Linux 计算机。

2. 打开 zip 文件，将 AdventureWorks2014.bak 文件提取到计算机上的文件夹。

## <a name="transfer-the-backup-file-to-linux"></a>将备份文件传输到 Linux

若要还原数据库，首先必须将备份文件从 Windows 计算机传输到目标 Linux 计算机。

1. 对于 Windows，需安装 Bash shell。 有以下几个选项：

   - 如下载一种开放源 Bash shell [PuTTY](http://www.putty.org/)。
   - 或者，在 Windows 10 中，使用新[内置 Bash shell (beta)](https://msdn.microsoft.com/en-us/commandline/wsl/about)。
   - 或者，如果你使用 Git，则使用[Git Bash shell](https://git-scm.com/downloads)。

2. 打开 Bash shell （终端） 并导航到目录包含**AdventureWorks2014.bak**。

3. 使用**scp** （安全的复制） 命令，以将文件传输到目标 Linux 计算机。 下面的示例传输**AdventureWorks2014.bak**到的主目录*user1*命名的服务器上*linuxserver1*。

   ```bash
   sudo scp AdventureWorks2014.bak user1@linuxserver1:./
   ```
   
   在上一示例中，可以改为提供 IP 地址来代替服务器名称。

有几种使用 scp 的替代方法。 一个是使用[Samba](https://help.ubuntu.com/community/Samba)设置一个 SMB 网络共享之间 Windows 和 Linux。 在 Ubuntu 上的演练，请参阅[如何创建网络共享通过 Samba](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!)。 建立后，您可以访问它为网络文件共享在 Windows 中，如 **\\ \\machinenameorip\\共享**。

## <a name="move-the-backup-file"></a>移动备份文件

此时，备份文件已在 Linux 服务器上。 在将数据库还原到 SQL Server 之前, 中，你必须将备份的子目录中**/var/opt/mssql**。

1. 在包含该备份的目标 Linux 计算机上打开终端。

2. 进入超级用户模式。

   ```bash
   sudo su
   ```

3. 创建新的备份目录。 如果目录已存在，-p 参数不会执行任何操作。

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

4. 将备份文件移动到该目录。 在下面的示例中，备份文件驻留在的主目录*user1*。 更改此命令，以匹配的位置， **AdventureWorks2014.bak**在您的计算机上。

   ```bash
   mv /home/user1/AdventureWorks2014.bak /var/opt/mssql/backup/
   ```

5. 退出超级用户模式。

   ```bash
   exit
   ```

## <a name="restore-the-database-backup"></a>还原数据库备份

要还原备份，可以使用 RESTORE DATABASE Transact-SQL (TQL) 命令。

> [!NOTE] 
> 下列步骤使用 sqlcmd 工具。 如果你尚未安装 SQL Server Tools，请参阅[在 Linux 上安装 SQL Server](sql-server-linux-setup.md)。

1. 在相同的终端中，启动**sqlcmd**。 下面的示例连接到具有的本地 SQL Server 实例*SA*用户。 出现提示时输入密码，或使用 -P 参数指定密码。

   ```bash
   sqlcmd -S localhost -U SA
   ```

2. 连接后，输入以下**还原数据库**命令，并在每一行后按 enter 键。 还原下面的示例**AdventureWorks2014.bak**文件从*/var/opt/mssql/backup*目录。

   ```sql
   RESTORE DATABASE AdventureWorks
   FROM DISK = '/var/opt/mssql/backup/AdventureWorks2014.bak'
   WITH MOVE 'AdventureWorks2014_Data' TO '/var/opt/mssql/data/AdventureWorks2014_Data.mdf',
   MOVE 'AdventureWorks2014_Log' TO '/var/opt/mssql/data/AdventureWorks2014_Log.ldf'
   GO
   ```

   应收到已成功还原数据库的消息。

3. 首先将上下文更改为 AdventureWorks 数据库来验证还原操作。 

   ```sql
   USE AdventureWorks
   GO
   ```

4. 运行以下查询，其中列出了前 10 种产品在**Production.Products**表。

   ```sql
   SELECT TOP 10 Name, ProductNumber FROM Production.Product ORDER BY Name
   GO
   ```

![Production.Products 查询输出](./media/sql-server-linux-migrate-restore-database/sql-server-linux-adventureworks-query.png)

## <a name="next-steps"></a>后续步骤

有关其他数据库和数据迁移方法的详细信息，请参阅[将数据库迁移到 SQL Server on Linux](sql-server-linux-migrate-overview.md)。 

