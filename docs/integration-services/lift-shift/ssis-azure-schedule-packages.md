---
title: "计划安排 Azure 上的 SSIS 包执行 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 26160f982982b1a8163662f57cb317e7252ab0e4
ms.sourcegitcommit: 6e016a4ffd28b09456008f40ff88aef3d911c7ba
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="schedule-the-execution-of-an-ssis-package-on-azure"></a>计划安排 Azure 上的 SSIS 包执行
可以通过选择以下计划安排选项之一，计划安排存储在 Azure SQL 数据库服务器上 SSISDB 目录数据库中的包的执行。
-   [SQL Server 代理](#agent)
-   [SQL 数据库弹性作业](#elastic)
-   [Azure 数据工厂 SQL Server 存储过程活动](#sproc)

## <a name="agent"></a> 使用 SQL Server 代理计划安排一个包

### <a name="prerequisite"></a>先决条件

必须先将 SQL 数据库服务器添加为链接服务器，才能在本地使用 SQL Server 代理来计划安排存储在 Azure SQL 数据库服务器上的包的执行。 有关详细信息，请参阅[创建链接服务器](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)和[链接服务器](../../relational-databases/linked-servers/linked-servers-database-engine.md)。

### <a name="create-a-sql-server-agent-job"></a>创建 SQL Server 代理作业

若要在本地使用 SQL Server 代理来计划安排一个包，请创建一个具有作业步骤的作业，该作业依次调用 SSIS 目录存储过程 `[catalog].[create_execution]` 和 `[catalog].[start_execution]`。 有关详细信息，请参阅[包的 SQL Server 代理作业](../packages/sql-server-agent-jobs-for-packages.md)。

1.  在 SQL Server Management Studio 中，连接到要在其中创建作业的本地 SQL Server 数据库。

2.  右键单击“SQL Server 代理”节点，选择“新建”，然后选择“作业”以打开“新建作业”对话框。

3.  在“新建作业”对话框中，选择“步骤”页，然后选择“新建”以打开“新建作业步骤”对话框。

4.  在“新建作业步骤”对话框中，选择 `SSISDB` 作为  **数据库。**

5.  在命令字段中，输入与下列示例所示的脚本类似的 Transact-SQL 脚本：

    ```sql
    DECLARE @return_value int, @exe_id bigint 

    EXEC @return_value = [YourLinkedServer].[SSISDB].[catalog].[create_execution] 
    @folder_name=N'folderName', @project_name=N'projectName', 
    @package_name=N'packageName', @use32bitruntime=0, 
    @runinscaleout=1, @useanyworker=1, @execution_id=@exe_id OUTPUT 
 
    EXEC [YourLinkedServer].[SSISDB].[catalog].[start_execution] @execution_id=@exe_id

    GO
    ```

6.  完成配置并计划作业。

## <a name="elastic"></a> 使用 SQL 数据库弹性作业计划安排一个包

有关 SQL 数据库上的弹性作业的详细信息，请参阅[管理横向扩展的云数据库](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)。

### <a name="prerequisites"></a>必备条件

在可以使用弹性作业来计划存储在 Azure SQL 数据库服务器上 SSISDB 目录数据库中的 SSIS 包之前，必须先完成以下操作：

1.  安装并配置弹性数据库作业组件。 有关详细信息，请参阅[安装弹性数据库作业概述](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-service-installation)。

2. 创建数据库范围的凭据，作业可使用该凭据将命令发送到 SSIS 目录数据库。 有关详细信息，请参阅 [CREATE DATABASE SCOPED CREDENTIAL（创建数据库范围的凭据）(Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)。

### <a name="create-an-elastic-job"></a>创建弹性作业

使用与下列示例所示的脚本类似的 Transact-SQL 脚本来创建作业：

```sql
-- Create Elastic Jobs target group 
EXEC jobs.sp_add_target_group 'TargetGroup' 

-- Add Elastic Jobs target group member 
EXEC jobs.sp_add_target_group_member @target_group_name='TargetGroup', 
    @target_type='SqlDatabase', @server_name='YourSQLDBServer.database.windows.net',
    @database_name='SSISDB' 

-- Add a job to schedule SSIS package execution
EXEC jobs.sp_add_job @job_name='ExecutePackageJob', @description='Description', 
    @schedule_interval_type='Minutes', @schedule_interval_count=60

-- Add a job step to create/start SSIS package execution using SSISDB catalog stored procedures
EXEC jobs.sp_add_jobstep @job_name='ExecutePackageJob', 
    @command=N'DECLARE @exe_id bigint 
        EXEC [SSISDB].[catalog].[create_execution]
            @folder_name=N''folderName'', @project_name=N''projectName'',
            @package_name=N''packageName'', @use32bitruntime=0,
            @runinscaleout=1, @useanyworker=1, 
            @execution_id=@exe_id OUTPUT         
        EXEC [SSISDB].[catalog].[start_execution] @exe_id, @retry_count=0', 
    @credential_name='YourDBScopedCredentials', 
    @target_group_name='TargetGroup' 

-- Enable the job schedule 
EXEC jobs.sp_update_job @job_name='ExecutePackageJob', @enabled=1, 
    @schedule_interval_type='Minutes', @schedule_interval_count=60 
```

## <a name="sproc"></a> 使用 Azure 数据工厂 SQL Server 存储过程活动计划安排一个包

要了解如何使用 Azure 数据工厂存储过程活动来安排 SSIS 包，请参阅下列文章：

-   对于数据工厂版本 2：[Invoke an SSIS package using stored procedure activity in Azure Data Factory](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-stored-procedure-activity)（在 Azure 数据工厂中使用存储过程活动调用 SSIS 包）

-   对于数据工厂版本 1：[Invoke an SSIS package using stored procedure activity in Azure Data Factory](https://docs.microsoft.com/azure/data-factory/v1/how-to-invoke-ssis-package-stored-procedure-activity)（在 Azure 数据工厂中使用存储过程活动调用 SSIS 包）

## <a name="next-steps"></a>后续步骤
有关 SQL Server 代理的详细信息，请参阅 [包的 SQL Server 代理作业](../packages/sql-server-agent-jobs-for-packages.md)。

有关 SQL 数据库上的弹性作业的详细信息，请参阅[管理横向扩展的云数据库](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)。
