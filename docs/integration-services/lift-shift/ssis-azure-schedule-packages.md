---
title: 计划安排 Azure 上的 SSIS 包 | Microsoft Docs
ms.date: 05/09/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.component: lift-shift
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4bfad00425848189d88bd780296db00ec810b37c
ms.sourcegitcommit: 0cc2cb281e467a13a76174e0d9afbdcf4ccddc29
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2018
---
# <a name="schedule-the-execution-of-an-ssis-package-in-azure"></a>计划安排 Azure 上的 SSIS 包执行
可以通过选择以下计划安排选项之一，计划安排存储在 Azure SQL 数据库服务器上 SSISDB 目录数据库中的包的执行。
-   [SQL Server Management Studio (SSMS) 中的计划安排选项](#ssms)
-   [Azure 数据工厂执行 SSIS 包活动](#execute)
-   [Azure 数据工厂 SQL Server 存储过程活动](#storedproc)
-   [SQL 数据库弹性作业](#elastic)
-   [SQL Server 代理](#agent)

## <a name="ssms"></a> 使用 SSMS 计划安排包

在 SQL Server Management Studio (SSMS) 中，可以右键单击部署到 SSIS 目录数据库 (SSISDB) 的包，并选择“计划”以打开“新建计划”对话框。 有关详细信息，请参阅[使用 SSMS 计划安排 Azure 上的 SSIS 包执行](ssis-azure-schedule-packages-ssms.md)。

此功能要求 SQL Server Management Studio 17.7 或更高版本。 若要获取 SSMS 最新版本，请参阅[下载 SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)。

## <a name="execute"></a> 通过“执行 SSIS 包”活动来计划安排包

有关如何在 Azure 数据工厂中使用“执行 SSIS 包”活动来计划安排 SSIS 包的信息，请参阅[在 Azure 数据工厂中使用 SSIS 活动运行 SSIS 包](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)。

## <a name="storedproc"></a> 使用“存储过程”活动来计划安排包

有关如何在 Azure 数据工厂中使用“存储过程”活动计划安排 SSIS 包的信息，请参阅[在 Azure 数据工厂中使用存储过程活动运行 SSIS 包](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-stored-procedure-activity)。

对于数据工厂版本 1，请参阅[在 Azure 数据工厂中使用存储过程活动运行 SSIS 包](https://docs.microsoft.com/azure/data-factory/v1/how-to-invoke-ssis-package-stored-procedure-activity)。

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

## <a name="agent"></a> 使用 SQL Server 代理计划安排一个包

### <a name="prerequisite---create-a-linked-server"></a>先决条件 - 创建链接服务器

必须先将 SQL 数据库服务器作为链接服务器添加到本地 SQL Server，才能在本地使用 SQL Server 代理来计划安排存储在 Azure SQL 数据库服务器上的包的执行。

1.  **设置链接服务器**

    ```sql
    -- Add the SSISDB database on your Azure SQL Database as a linked server to your SQL Server on premises
    EXEC sp_addlinkedserver
        @server='myLinkedServer', -- Name your linked server
        @srvproduct='',     
        @provider='sqlncli', -- Use SQL Server native client
        @datasrc='<server_name>.database.windows.net', -- Add your Azure SQL Database server endpoint
        @location=‘’,
        @provstr=‘’,
        @catalog='SSISDB'  -- Add SSISDB as the initial catalog
    ```

2.  **设置链接服务器凭据**

    ```sql
    -- Add your Azure SQL DB server admin credentials
    EXEC sp_addlinkedsrvlogin
        @rmtsrvname = 'myLinkedServer’,
        @useself = 'false’,
        @rmtuser = 'myUsername', -- Add your server admin username
        @rmtpassword = 'myPassword' -- Add your server admin password
    ```

3.  **设置链接服务器选项**

    ```sql
    EXEC sp_serveroption 'myLinkedServer', 'rpc out', true;
    ```

有关详细信息，请参阅[创建链接服务器](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)和[链接服务器](../../relational-databases/linked-servers/linked-servers-database-engine.md)。

### <a name="create-a-sql-server-agent-job"></a>创建 SQL Server 代理作业

若要在本地使用 SQL Server 代理来计划安排一个包，请创建一个具有作业步骤的作业，该作业依次调用 SSIS 目录存储过程 `[catalog].[create_execution]` 和 `[catalog].[start_execution]`。 有关详细信息，请参阅[包的 SQL Server 代理作业](../packages/sql-server-agent-jobs-for-packages.md)。

1.  在 SQL Server Management Studio 中，连接到要在其中创建作业的本地 SQL Server 数据库。

2.  右键单击“SQL Server 代理”节点，选择“新建”，然后选择“作业”以打开“新建作业”对话框。

3.  在“新建作业”对话框中，选择“步骤”页，然后选择“新建”以打开“新建作业步骤”对话框。

4.  在“新建作业步骤”对话框中，选择 `SSISDB` 作为  **数据库。**

5.  在“命令”字段中，输入与以下示例所示脚本类似的 Transact-SQL 脚本：

    ```sql
    -- T-SQL script to create and start SSIS package execution using SSISDB stored procedures
    DECLARE @return_value int, @exe_id bigint 

    EXEC @return_value = [YourLinkedServer].[SSISDB].[catalog].[create_execution] 
        @folder_name=N'folderName', @project_name=N'projectName', 
        @package_name=N'packageName', @use32bitruntime=0, @runincluster=1, @useanyworker=1,
        @execution_id=@exe_id OUTPUT 

    EXEC [YourLinkedServer].[SSISDB].[catalog].[set_execution_parameter_value] @exe_id,
        @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1

    EXEC [YourLinkedServer].[SSISDB].[catalog].[start_execution] @execution_id=@exe_id
    ```

6.  完成配置并计划作业。

## <a name="next-steps"></a>后续步骤
有关 SQL Server 代理的详细信息，请参阅 [包的 SQL Server 代理作业](../packages/sql-server-agent-jobs-for-packages.md)。

有关 SQL 数据库上的弹性作业的详细信息，请参阅[管理横向扩展的云数据库](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)。
