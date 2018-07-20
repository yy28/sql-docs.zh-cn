---
title: 将 SQL Server 数据库从 Windows 迁移到 Linux |Microsoft Docs
description: 本教程演示如何在 Windows 上进行 SQL Server 数据库备份并将其还原到运行 SQL Server 2017 的 Linux 计算机。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/16/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.openlocfilehash: 8cc1010f2492054a467abfc53e859d39a86e1c78
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086699"
---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>使用备份和还原将 SQL Server 数据库从 Windows 迁移到 Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server 的备份和还原功能是从 Windows 上的 SQL Server 数据库迁移到 SQL Server 2017 Linux 上的推荐的方法。 在本教程中，将会演练数据库移到 Linux，使用备份和还原技术所需的步骤。

> [!div class="checklist"]
> * 使用 SSMS 创建 Windows 上的备份文件
> * 在 Windows 上安装 Bash shell
> * 从 Bash shell 中将备份文件移到 Linux
> * 在 Linux 上使用 TRANSACT-SQL 将备份文件还原
> * 运行查询来验证迁移

此外可以创建 SQL Server Always On 可用性组以将 SQL Server 数据库从 Windows 迁移到 Linux。 请参阅[sql-server-linux-availability-group-cross-platform](sql-server-linux-availability-group-cross-platform.md)。

## <a name="prerequisites"></a>必要條件

完成本教程需要满足以下先决条件：

* 使用以下 Windows 计算机：
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions)安装。
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)安装。
  * 要迁移的目标数据库。

* 使用以下安装的 Linux 计算机：
  * SQL Server 2017 ([RHEL](quickstart-install-connect-red-hat.md)， [SLES](quickstart-install-connect-suse.md)，或[Ubuntu](quickstart-install-connect-ubuntu.md)) 使用命令行工具。

## <a name="create-a-backup-on-windows"></a>Windows 上创建备份

有几种方法在 Windows 上创建数据库的备份文件。 以下步骤使用 SQL Server Management Studio (SSMS)。

1. 启动**SQL Server Management Studio**在 Windows 计算机上。

1. 在连接对话框中，输入**localhost**。

1. 在对象资源管理器，展开**数据库**。

1. 右键单击目标数据库中，选择**任务**，然后单击**备份...**.

   ![使用 SSMS 创建备份文件](./media/sql-server-linux-migrate-restore-database/ssms-create-backup.png)

1. 在**数据库备份**对话框中，确认**备份类型**是**完整**并**备份到**是**磁盘**. 请注意名称和文件的位置。 例如，一个名为的数据库**YourDB** SQL Server 2016 上都具有一个默认备份路径的`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak`。

1. 单击**确定**来备份数据库。

> [!NOTE]
> 另一种方法是运行 TRANSACT-SQL 查询以创建备份文件。 以下 TRANSACT-SQL 命令对数据库执行与前面的步骤相同的操作称为**YourDB**:
>
> ```sql
> BACKUP DATABASE [YourDB] TO  DISK =
> N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak'
> WITH NOFORMAT, NOINIT, NAME = N'YourDB-Full Database Backup',
> SKIP, NOREWIND, NOUNLOAD, STATS = 10
> GO
> ```

## <a name="install-a-bash-shell-on-windows"></a>在 Windows 上安装 Bash shell

若要还原数据库，首先必须将备份文件从 Windows 计算机传输到目标 Linux 计算机。 在本教程中，我们将文件移到 Linux 从 Bash shell （终端窗口中） 在 Windows 上运行。

1. 支持在 Windows 计算机上安装 Bash shell **scp** （安全复制） 和**ssh** （远程登录名） 命令。 两个示例包括：

   * [适用于 Linux 的 Windows 子系统](https://msdn.microsoft.com/commandline/wsl/about)(Windows 10)
   * Git Bash Shell ([https://git-scm.com/downloads](https://git-scm.com/downloads))

1. 在 Windows 上打开的 Bash 会话。

## <a id="scp"></a> 将备份文件复制到 Linux

1. 在 Bash 会话中，导航到包含您的备份文件的目录。 例如：

   ```bash
   cd 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\'
   ```

1. 使用**scp**命令以将文件传输到目标 Linux 计算机。 以下示例中传输**YourDB.bak**到主目录*user1* Linux 服务器的 IP 地址上*192.0.2.9*:

   ```bash
   scp YourDB.bak user1@192.0.2.9:./
   ```
   ![scp 命令](./media/sql-server-linux-migrate-restore-database/scp-command.png)

> [!TIP]
> 没有为文件传输使用 scp 的替代方法。 一种是使用[Samba](https://help.ubuntu.com/community/Samba)来配置 Windows 和 Linux 之间 SMB 网络共享。 在 Ubuntu 上的演练，请参阅[如何创建网络共享通过 Samba](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!)。 一旦建立，您可以访问它为网络文件共享从 Windows，如 **\\ \\machinenameorip\\共享**。

## <a name="move-the-backup-file-before-restoring"></a>在还原之前移动备份文件

此时，备份文件是在用户的主目录在 Linux 服务器上。 之前将数据库还原到 SQL Server，你必须将备份置于的子目录 **/var/opt/mssql**。

1. 在同一个 Windows Bash 会话中，远程连接到使用在目标 Linux 计算机**ssh**。 以下示例连接到 Linux 计算机**192.0.2.9**以用户身份**user1**。

   ```bash
   ssh user1@192.0.2.9
   ```

   你现在远程的 Linux 服务器上运行命令。

1. 进入超级用户模式。

   ```bash
   sudo su
   ```

1. 创建新的备份目录。 如果目录已存在，-p 参数不会执行任何操作。

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

1. 将备份文件移动到该目录。 在以下示例中，备份文件驻留在的主目录*user1*。 更改要与您的备份文件的位置和文件名称匹配的命令。

   ```bash
   mv /home/user1/YourDB.bak /var/opt/mssql/backup/
   ```

1. 退出超级用户模式。

   ```bash
   exit
   ```

## <a name="restore-your-database-on-linux"></a>Linux 上的将数据库还原

若要还原数据库备份，可以使用**RESTORE DATABASE** TRANSACT-SQL (TQL) 命令。

> [!NOTE]
> 以下步骤使用**sqlcmd**工具。 如果尚未安装 SQL Server Tools，请参阅[Linux 上的安装 SQL Server 命令行工具](sql-server-linux-setup-tools.md)。

1. 在同一终端中，启动**sqlcmd**。 以下示例连接到本地 SQL Server 实例与**SA**用户。 输入的密码，出现提示时，或通过添加指定的密码 **-P**参数。

   ```bash
   sqlcmd -S localhost -U SA
   ```

1. 在`>1`提示符下，输入以下**RESTORE DATABASE**命令，并在每行 （不能复制并粘贴整个多行命令在一次） 后按 enter 键。 替换所有出现的`YourDB`与数据库的名称。

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```

   应收到已成功还原数据库的消息。

1. 通过列出所有服务器上的数据库来验证还原操作。 应列出已还原的数据库。

   ```sql
   SELECT Name FROM sys.Databases
   GO
   ```

1. 你已迁移的数据库上运行其他查询。 以下命令切换到上下文**YourDB**数据库和从其表中选择行。

   ```sql
   USE YourDB
   SELECT * FROM YourTable
   GO
   ```

1. 完成后使用**sqlcmd**，类型`exit`。

1. 完成后在远程工作**ssh**会话中，键入`exit`试。

## <a name="next-steps"></a>后续步骤

在本教程中，您学习了如何在 Windows 上备份数据库并将其移到运行 SQL Server 2017 的 Linux 服务器。 你将了解到：
> [!div class="checklist"]
> * 使用 SSMS 和 Transact SQL 创建 Windows 上的备份文件
> * 在 Windows 上安装 Bash shell
> * 使用**scp**将备份文件从 Windows 移到 Linux
> * 使用**ssh**以远程方式连接到 Linux 计算机
> * 重新定位要准备用于还原的备份文件
> * 使用**sqlcmd**运行 Transact-SQL 命令
> * 使用数据库备份还原**RESTORE DATABASE**命令 
> * 运行查询以验证迁移

接下来，浏览其他迁移方案适用于 SQL Server Linux 上。 

> [!div class="nextstepaction"]
>[将数据库迁移到 Linux 上的 SQL Server](sql-server-linux-migrate-overview.md)
