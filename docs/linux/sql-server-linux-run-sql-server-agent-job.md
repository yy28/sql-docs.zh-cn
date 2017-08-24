---
title: "创建并在 Linux 上运行 SQL Server 作业 |Microsoft 文档"
description: "本教程演示如何在 Linux 上运行 SQL Server 代理作业。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 1d93d95e-9c89-4274-9b3f-fa2608ec2792
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3ffb76838940f42d7a696e1c17f227517d89012d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="create-and-run-sql-server-agent-jobs-on-linux"></a>在 Linux 上创建和运行 SQL Server 代理作业

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

SQL Server 作业用于定期执行 SQL Server 数据库中相同的命令序列。 本主题提供使用 Transact-SQL 和 SQL Server Management Studio (SSMS) 在 Linux 上创建 SQL Server 代理作业的示例。

有关与 SQL Server 代理在此版本中的已知问题，请参阅[发行说明](sql-server-linux-release-notes.md)。

## <a name="prerequisites"></a>必要條件 
若要创建和运行作业，必须首先安装 SQL Server 代理服务。 有关安装说明，请参阅[SQL Server 代理安装主题](sql-server-linux-setup-sql-agent.md)。

## <a name="create-a-job-with-transact-sql"></a>使用 Transact-SQL 创建作业

以下步骤提供在 Linux 上使用 Transact-SQL 命令创建 SQL Server 代理作业的示例。 在此示例中的这些作业在示例数据库上运行每日备份`SampleDB`。 


> [!TIP]
> 可以使用任何 T-SQL 客户端运行这些命令。 例如，在 Linux 上你可以使用[sqlcmd](sql-server-linux-setup-tools.md)或[Visual Studio Code](sql-server-linux-develop-use-vscode.md)。 在远程 Windows Server 中，还可以在 SQL Server Management Studio (SSMS) 中运行查询，或使用 UI 接口进行作业管理，下一部分将对此进行说明。

1. **创建作业**。 下面的示例使用[sp_add_job](https://msdn.microsoft.com/library/ms182079.aspx)创建一个名为作业`Daily AdventureWorks Backup`。

    ```tsql
     -- Adds a new job executed by the SQLServerAgent service 
     -- called 'Daily SampleDB Backup'  
     CREATE DATABASE SampleDB
     USE msdb ;  
     GO  
     EXEC dbo.sp_add_job  
         @job_name = N'Daily SampleDB Backup' ;  
     GO

    ```

2. **添加一个或多个作业步骤**。 下面的 TRANSACT-SQL 脚本使用[sp_add_jobstep](https://msdn.microsoft.com/library/ms187358.aspx)创建可创建的备份的作业步骤`AdventureWlorks2014`数据库。

    ```tsql
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

3. **创建作业计划**。 此示例使用[sp_add_schedule](https://msdn.microsoft.com/library/ms366342.aspx)若要创建的作业每日计划。

    ```tsql
    -- Creates a schedule called 'Daily'  
    EXEC dbo.sp_add_schedule  
     @schedule_name = N'Daily SampleDB',  
     @freq_type = 4,  
     @freq_interval = 1,
     @active_start_time = 233000 ;  
   USE msdb ;  
   GO
    ```

4. **将作业计划附加到作业**。 使用[sp_attach_schedule](https://msdn.microsoft.com/library/ms186766.aspx)要附加到作业的作业计划。

    ```tsql
    -- Sets the 'Daily' schedule to the 'Daily AdventureWorks Backup' Job  
    EXEC sp_attach_schedule  
     @job_name = N'Daily SampleDB Backup',  
     @schedule_name = N'Daily SampleDB';  
    GO
    ```

5. **将作业分配到目标服务器**。 将作业分配到目标服务器与[sp_add_jobserver](https://msdn.microsoft.com/library/ms178625.aspx)。 此示例中的目标是本地服务器。

    ```tsql
    EXEC dbo.sp_add_jobserver  
     @job_name = N'Daily SampleDB Backup',  
     @server_name = N'(LOCAL)';  
    GO
    ```
6. **启动作业**。 

    ```tsql
    EXEC dbo.sp_start_job N' Daily SampleDB Backup' ;
    GO
    ```
## <a name="create-a-job-with-ssms"></a>使用 SSMS 创建作业

还可以在 Windows 上使用 SQL Server Management Studio (SSMS) 远程创建和管理作业。

1. **在 Windows 上启动 SSMS 并连接到 Linux SQL Server 实例。** 有关详细信息，请参阅[上 Linux 使用 SSMS 管理 SQL Server](sql-server-linux-develop-use-ssms.md)。

1. **创建新的数据库名为 SampleDB**。

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-0.png" alt="Create a SampleDB database" style="width: 550px;"/>

2. **验证 SQL 代理已安装并正确配置。** 查找在对象资源管理器中的 SQL Server 代理旁边的加号。 如果未安装 SQL Server 代理，请参阅[在 Linux 上安装 SQL Server 代理](sql-server-linux-setup-sql-agent.md)。

    ![验证 SQL Server 代理已安装](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-1.png)


3. **创建新的作业。**

    ![创建新的作业](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-2.png)


4. **为你的作业提供一个名称并创建作业步骤。**

    ![创建作业步骤](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-3.png)


5. **指定你想要使用哪些子系统和作业步骤应执行的操作。**

    ![作业子系统](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-4.png)

    ![作业步骤操作](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-5.png)

6. **创建新的作业计划。**

    ![作业计划](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-6.png)
  
    ![作业计划](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-8.png)

7. **启动你的作业。**

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-9.png" alt="Start the SQL Server Agent job" style="width: 550px;"/>

## <a name="next-steps"></a>后续步骤

有关创建和管理 SQL Server 代理作业的详细信息，请参阅[SQL Server 代理](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)。

