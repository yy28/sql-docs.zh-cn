---
title: 创建和运行 SQL Server Linux 上的作业 |Microsoft Docs
description: 本教程演示如何在 Linux 上运行 SQL Server 代理作业。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 1d93d95e-9c89-4274-9b3f-fa2608ec2792
ms.openlocfilehash: 162015772bb54023816fcc7d911ca34fbd4a3ac7
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38001799"
---
# <a name="create-and-run-sql-server-agent-jobs-on-linux"></a>在 Linux 上创建和运行 SQL Server 代理作业

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server 作业用于定期执行 SQL Server 数据库中相同的命令序列。 本教程提供了如何在 Linux 上创建 SQL Server 代理作业的示例使用 TRANSACT-SQL 和 SQL Server Management Studio (SSMS)。

> [!div class="checklist"]
> * 在 Linux 上安装 SQL Server 代理
> * 创建一个新作业来执行每日数据库备份
> * 计划和运行作业
> * 在 SSMS （可选） 中执行相同的步骤

Linux 上的 SQL Server 代理的已知问题，请参阅[发行说明](sql-server-linux-release-notes.md)。

## <a name="prerequisites"></a>必要條件

完成本教程需要满足以下先决条件：

* Linux 计算机满足以下先决条件：
  * SQL Server 2017 ([RHEL](quickstart-install-connect-red-hat.md)， [SLES](quickstart-install-connect-suse.md)，或[Ubuntu](quickstart-install-connect-ubuntu.md)) 使用命令行工具。

以下系统必备组件是可选的：

* 使用 SSMS 的 Windows 计算机：
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)有关 SSMS 的可选步骤。

## <a name="enable-sql-server-agent"></a>启用 SQL Server 代理

若要在 Linux 上使用 SQL Server 代理，必须首先已安装的 SQL Server 2017 的计算机上启用 SQL Server 代理。

1. 若要启用 SQL Server 代理，请执行以下步骤。
  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
  ```

1. 使用以下命令重新启动 SQL Server:
  ```bash
  sudo systemctl restart mssql-server
  ```

> [!NOTE]
> 从 SQL Server 2017 CU4 开始，SQL Server 代理是附带**mssql server**打包并默认处于禁用状态。 为代理 CU4 访问之前就设置起来[Linux 上安装 SQL Server 代理](sql-server-linux-setup-sql-agent.md)。

## <a name="create-a-sample-database"></a>创建示例数据库

使用以下步骤创建一个名为的示例数据库**SampleDB**。 此数据库用于每日备份作业。

1. 在 Linux 计算机上打开 bash 终端会话。

1. 使用**sqlcmd**运行 Transact SQL **CREATE DATABASE**命令。

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'CREATE DATABASE SampleDB'
   ```

1. 验证通过列出你的服务器上的数据库创建数据库。

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'SELECT Name FROM sys.Databases'
   ```

## <a name="create-a-job-with-transact-sql"></a>使用 Transact-SQL 创建作业

以下步骤使用 TRANSACT-SQL 命令创建在 Linux 上的 SQL Server 代理作业。 在作业运行的示例数据库中，每日备份**SampleDB**。

> [!TIP]
> 可以使用任何 T-SQL 客户端运行这些命令。 例如，在 Linux 上您可以使用[sqlcmd](sql-server-linux-setup-tools.md)或[Visual Studio Code](sql-server-linux-develop-use-vscode.md)。 在远程 Windows Server 中，还可以在 SQL Server Management Studio (SSMS) 中运行查询，或使用 UI 接口进行作业管理，下一部分将对此进行说明。

1. 使用[sp_add_job](../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)若要创建一个名为作业`Daily SampleDB Backup`。

   ```sql
   -- Adds a new job executed by the SQLServerAgent service
   -- called 'Daily SampleDB Backup'
   USE msdb ;
   GO
   EXEC dbo.sp_add_job
      @job_name = N'Daily SampleDB Backup' ;
   GO
   ```

1. 调用[sp_add_jobstep](../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)若要创建的备份创建的作业步骤`SampleDB`数据库。

   ```sql
   -- Adds a step (operation) to the job
   EXEC sp_add_jobstep
      @job_name = N'Daily SampleDB Backup',
      @step_name = N'Backup database',
      @subsystem = N'TSQL',
      @command = N'BACKUP DATABASE SampleDB TO DISK = \
         N''/var/opt/mssql/data/SampleDB.bak'' WITH NOFORMAT, NOINIT, \
         NAME = ''SampleDB-full'', SKIP, NOREWIND, NOUNLOAD, STATS = 10',
      @retry_attempts = 5,
      @retry_interval = 5 ;
   GO
   ```

1. 然后创建与作业的每日计划[sp_add_schedule](../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md)。

   ```sql
   -- Creates a schedule called 'Daily'
   EXEC dbo.sp_add_schedule
      @schedule_name = N'Daily SampleDB',
      @freq_type = 4,
      @freq_interval = 1,
      @active_start_time = 233000 ;
   USE msdb ;
   GO
   ```

1. 将作业计划附加到作业[sp_attach_schedule](../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)。

   ```sql
   -- Sets the 'Daily' schedule to the 'Daily SampleDB Backup' Job
   EXEC sp_attach_schedule
      @job_name = N'Daily SampleDB Backup',
      @schedule_name = N'Daily SampleDB';
   GO
   ```

1. 使用[sp_add_jobserver](../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)若要将作业分配到目标服务器。 在此示例中，目标是本地服务器。

   ```sql
   EXEC dbo.sp_add_jobserver
      @job_name = N'Daily SampleDB Backup',
      @server_name = N'(LOCAL)';
   GO
   ```
1. 启动的作业[sp_start_job](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)。

   ```sql
   EXEC dbo.sp_start_job N' Daily SampleDB Backup' ;
   GO
   ```

## <a name="create-a-job-with-ssms"></a>使用 SSMS 创建作业

还可以在 Windows 上使用 SQL Server Management Studio (SSMS) 远程创建和管理作业。

1. 在 Windows 上启动 SSMS 并连接到 Linux SQL Server 实例。 有关详细信息，请参阅[在 Linux 上使用 SSMS 管理 SQL Server](sql-server-linux-manage-ssms.md)。

1. 验证是否已创建一个名为的示例数据库**SampleDB**。

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-0.png" alt="Create a SampleDB database" style="width: 550px;"/>

1. 验证 SQL 代理是否[安装](sql-server-linux-setup-sql-agent.md)并正确配置。 查找在对象资源管理器中的 SQL Server 代理旁边的加号。 如果未启用 SQL Server 代理，请尝试重新启动**mssql server** Linux 上的服务。

   ![验证安装了 SQL Server 代理](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-1.png)

1. 新建作业。

   ![创建新的作业](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-2.png)

1. 指定作业名称并创建作业步骤。

   ![创建作业步骤](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-3.png)

1. 指定要使用的子系统和应执行的作业步骤。

   ![作业子系统](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-4.png)

   ![作业步骤操作](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-5.png)

1. 新建作业计划。

   ![作业计划](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-6.png)

   ![作业计划](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-8.png)

1. 启动作业。

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-9.png" alt="Start the SQL Server Agent job" style="width: 550px;"/>

## <a name="next-steps"></a>后续步骤

在本教程中，您学习了如何：

> [!div class="checklist"]
> * 在 Linux 上安装 SQL Server 代理
> * 使用 TRANSACT-SQL 和系统存储过程来创建作业
> * 创建执行每日数据库备份的作业
> * 使用 SSMS UI 来创建和管理作业

接下来，了解创建和管理作业的其他功能：

> [!div class="nextstepaction"]
>[SQL Server 代理文档](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)
