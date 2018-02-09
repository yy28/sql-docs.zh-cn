---
title: "从 Windows 的 SQL Server 数据库迁移到 Linux |Microsoft 文档"
description: "本教程演示如何在 Windows 上，执行 SQL Server 数据库备份并将其还原到运行 SQL Server 2017 Linux 计算机。"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/16/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.workload: On Demand
ms.openlocfilehash: f50be15e4d778ffb9c77caa375dc6b963b5821cd
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>使用备份和还原将 SQL Server 数据库从 Windows 迁移到 Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server 的备份和还原功能是将从在 Windows 上的 SQL Server 数据库迁移到 SQL Server 自 2017 年在 Linux 上的推荐的方式。 在本教程中，将会演练使用备份将数据库移到 Linux 和还原技术所需的步骤。

> [!div class="checklist"]
> * 使用 SSMS 创建在 Windows 上的一个备份文件
> * 在 Windows 上安装的 Bash shell
> * 将备份文件从 Bash shell 移至 Linux
> * 还原与 TRANSACT-SQL 的 Linux 上的备份文件
> * 运行查询以验证迁移

你还可以创建 SQL Server Alwayson 可用性组将从 Windows 的 SQL Server 数据库迁移到 Linux。 请参阅[sql-server-linux-availability-group-cross-platform](sql-server-linux-availability-group-cross-platform.md)。

## <a name="prerequisites"></a>必要條件

完成本教程所需的以下先决条件：

* 替换为以下的 Windows 计算机：
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions)安装。
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)安装。
  * 要迁移的目标数据库。

* 具有安装以下版本的 Linux 计算机：
  * SQL Server 2017 ([RHEL](quickstart-install-connect-red-hat.md)， [SLES](quickstart-install-connect-suse.md)，或[Ubuntu](quickstart-install-connect-ubuntu.md)) 使用命令行工具。

## <a name="create-a-backup-on-windows"></a>在 Windows 上创建备份

有多种方法可以在 Windows 上创建数据库的备份文件。 以下步骤使用 SQL Server Management Studio (SSMS)。

1. 启动**SQL Server Management Studio** Windows 计算机上。

1. 在连接对话框中，输入**localhost**。

1. 在对象资源管理器，展开**数据库**。

1. 右键单击目标数据库中，选择**任务**，然后单击**备份...**.

   ![使用 SSMS 创建备份文件](./media/sql-server-linux-migrate-restore-database/ssms-create-backup.png)

1. 在**数据库备份**对话框中，验证**备份类型**是**完整**和**备份到**是**磁盘**。 记下名称和文件的位置。 例如，一个名为的数据库**YourDB** SQL Server 2016 上都具有的默认备份路径`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak`。

1. 单击**确定**以备份数据库。

> [!NOTE]
> 另一个选项是运行 TRANSACT-SQL 查询以创建备份文件。 以下 TRANSACT-SQL 命令对数据库执行相同操作作为前面的步骤调用**YourDB**:
>
> ```sql
> BACKUP DATABASE [YourDB] TO  DISK =
> N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak'
> WITH NOFORMAT, NOINIT, NAME = N'YourDB-Full Database Backup',
> SKIP, NOREWIND, NOUNLOAD, STATS = 10
> GO
> ```

## <a name="install-a-bash-shell-on-windows"></a>在 Windows 上安装的 Bash shell

若要还原数据库，首先必须将备份文件从 Windows 计算机传输到目标 Linux 计算机。 在本教程中，我们将文件移动到 Linux 从 Bash shell （终端窗口） 在 Windows 上运行。

1. 在您支持的 Windows 计算机上安装的 Bash shell **scp** （安全副本） 和**ssh** （远程登录名） 命令。 两个示例包括：

   * [适用于 Linux 的 Windows 子系统](https://msdn.microsoft.com/commandline/wsl/about)(Windows 10)
   * Git Bash Shell ([https://git-scm.com/downloads](https://git-scm.com/downloads))

1. 在 Windows 上打开 Bash 会话。

## <a id="scp"></a>将备份文件复制到 Linux

1. 在 Bash 会话中，导航到包含您的备份文件的目录。 例如：

   ```bash
   cd 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\'
   ```

1. 使用**scp**命令以将文件传输到目标 Linux 计算机。 下面的示例传输**YourDB.bak**到的主目录*user1* Linux 服务器的 IP 地址上*192.0.2.9*:

   ```bash
   scp YourDB.bak user1@192.0.2.9:./
   ```
   ![scp 命令](./media/sql-server-linux-migrate-restore-database/scp-command.png)

> [!TIP]
> 没有为文件传输使用 scp 的替代方法。 一个是使用[Samba](https://help.ubuntu.com/community/Samba)来配置 SMB 网络共享之间 Windows 和 Linux。 在 Ubuntu 上的演练，请参阅[如何创建网络共享通过 Samba](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!)。 建立后，您可以访问它为网络文件共享在 Windows 中，如 **\\ \\machinenameorip\\共享**。

## <a name="move-the-backup-file-before-restoring"></a>移动恢复之前的备份文件

此时，备份文件是在用户的主目录中的 Linux 服务器上。 在将数据库还原到 SQL Server 之前, 中，你必须将备份的子目录中**/var/opt/mssql**。

1. 在相同的 Windows Bash 会话中，远程连接到你的目标 Linux 计算机进行**ssh**。 下面的示例连接到 Linux 计算机**192.0.2.9**以用户身份**user1**。

   ```bash
   ssh user1@192.0.2.9
   ```

   现在远程的 Linux 服务器上运行命令。

1. 进入超级用户模式。

   ```bash
   sudo su
   ```

1. 创建新的备份目录。 如果目录已存在，-p 参数不会执行任何操作。

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

1. 将备份文件移动到该目录。 在下面的示例中，备份文件驻留在的主目录*user1*。 更改此命令，以匹配您的备份文件的位置和文件名称。

   ```bash
   mv /home/user1/YourDB.bak /var/opt/mssql/backup/
   ```

1. 退出超级用户模式。

   ```bash
   exit
   ```

## <a name="restore-your-database-on-linux"></a>在 Linux 上的将数据库还原

若要还原数据库备份，你可以使用**RESTORE DATABASE** TRANSACT-SQL (TQL) 命令。

> [!NOTE]
> 以下步骤使用**sqlcmd**工具。 如果你尚未安装 SQL Server Tools，请参阅[在 Linux 上的安装 SQL Server 命令行工具](sql-server-linux-setup-tools.md)。

1. 在相同的终端中，启动**sqlcmd**。 下面的示例连接到具有的本地 SQL Server 实例**SA**用户。 输入的密码出现提示时，或通过添加指定的密码**-P**参数。

   ```bash
   sqlcmd -S localhost -U SA
   ```

1. 在`>1`提示符下，输入以下**RESTORE DATABASE**命令，每个行 （不能复制并粘贴整个多行命令一次） 后按 enter 键。 将出现的所有`YourDB`替换为你的数据库的名称。

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```

   应收到已成功还原数据库的消息。

1. 通过列出所有服务器上的数据库来验证还原操作。 应列出还原的数据库。

   ```sql
   SELECT Name FROM sys.Databases
   GO
   ```

1. 在你迁移的数据库上运行其他查询。 以下命令切换到上下文**YourDB**数据库和从其表之一中选择行。

   ```sql
   USE YourDB
   SELECT * FROM YourTable
   GO
   ```

1. 完成后使用**sqlcmd**，类型`exit`。

1. 完成后在远程工作**ssh**会话中，键入`exit`试。

## <a name="next-steps"></a>后续步骤

在本教程中，您学习了如何在 Windows 上备份数据库并将其移到运行 SQL Server 自 2017 年的 Linux 服务器。 你应该了解一下如何到：
> [!div class="checklist"]
> * 使用 SSMS 和 Transact SQL 创建 Windows 上的备份文件
> * 在 Windows 上安装的 Bash shell
> * 使用**scp**将备份文件从 Windows 到 Linux
> * 使用**ssh**以远程方式连接到 Linux 计算机
> * 重新定位要准备还原的备份文件
> * 使用**sqlcmd**运行 TRANSACT-SQL 命令
> * 还原数据库备份与**RESTORE DATABASE**命令 
> * 运行查询以验证迁移

接下来，将介绍其他迁移方案适用于 SQL Server 上 Linux。 

> [!div class="nextstepaction"]
>[将数据库迁移到在 Linux 上的 SQL Server](sql-server-linux-migrate-overview.md)
