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
ms.openlocfilehash: 80fac355ad3ecc1486257651999be9d3f6ad30e6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="schedule-the-execution-of-an-ssis-package-on-azure"></a>计划安排 Azure 上的 SSIS 包执行
可以通过选择以下计划安排选项之一，计划安排存储在 Azure SQL 数据库服务器上 SSISDB 目录数据库中的包的执行。
-   [SQL Server 代理](#agent)
-   [SQL 数据库弹性作业](#elastic)
-   [Azure 数据工厂 SQL Server 存储过程活动](#sproc)

## <a name="agent"></a> 使用 SQL Server 代理计划安排一个包

### <a name="prerequisite"></a>前提条件

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

有关 SQL 数据库上的弹性作业的详细信息，请参阅[管理横向扩展的云数据库](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-overview)。

### <a name="prerequisites"></a>先决条件

在可以使用弹性作业来计划存储在 Azure SQL 数据库服务器上 SSISDB 目录数据库中的 SSIS 包之前，必须先完成以下操作：

1.  安装并配置弹性数据库作业组件。 有关详细信息，请参阅[安装弹性数据库作业概述](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-service-installation)。

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

> [!IMPORTANT]
> 将下例中的 JSON 脚本与 Azure 数据工厂版本 1 存储过程活动结合使用。

若要使用 Azure 数据工厂 SQL Server 存储过程活动来计划包，请完成以下操作：

1.  创建数据工厂。

2.  为承载 SSISDB 的 SQL 数据库创建一个链接服务。

3.  创建用于驱动计划的输出数据集。

4.  创建数据工厂管道，该管道使用 SQL Server 存储过程活动来运行 SSIS 包。

本部分概括介绍了这些步骤。 本文不提供完整的数据工厂教程。 如需了解详细信息，请参阅 [SQL Server 存储过程活动](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-stored-proc-activity)。

### <a name="created-a-linked-service-for-the-sql-database-that-hosts-ssisdb"></a>创建用于承载 SSISDB 的 SQL 数据库的链接服务
借助此链接服务，数据工厂可连接到 SSISDB。

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "description": "",
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Data Source = tcp: YourSQLDBServer.database.windows.net, 1433; Initial Catalog = SSISDB; User ID = YourUsername; Password = YourPassword; Integrated Security = False; Encrypt = True; Connect Timeout = 30"
        }
    }
}
```

### <a name="create-an-output-dataset"></a>创建输出数据集
输出数据集包含计划信息。

```json
{
    "name": "sprocsampleout",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
### <a name="create-a-data-factory-pipeline"></a>创建数据工厂管道
管道使用 SQL Server 存储过程活动运行 SSIS 包。

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [{
            "name": "SprocActivitySample",
            "type": "SqlServerStoredProcedure",
            "typeProperties": {
                "storedProcedureName": "sp_executesql",
                "storedProcedureParameters": {
                    "stmt": "Transact-SQL script to create and start SSIS package execution using SSISDB catalog stored procedures"
                }
            },
            "outputs": [{
                "name": "sprocsampleout"
            }],
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            }
        }],
        "start": "2017-10-01T00:00:00Z",
        "end": "2017-10-01T05:00:00Z",
        "isPaused": false
    }
}
```

不必创建新的存储过程来封装创建和启动 SSIS 包执行时所需的 Transact-SQL 命令。 可提供整个脚本，作为前述 JSON 示例中 `stmt` 参数的值。 下面是一个示例脚本：

```sql
-- T-SQL script to create and start SSIS package execution using SSISDB catalog stored procedures
DECLARE @return_value INT,@exe_id BIGINT,@err_msg NVARCHAR(150)

-- Create the exectuion
EXEC @return_value=[SSISDB].[catalog].[create_execution] @folder_name=N'folderName', @project_name=N'projectName', @package_name=N'packageName', @use32bitruntime=0, @runinscaleout=1,@useanyworker=1, @execution_id=@exe_id OUTPUT

-- To synchronize SSIS package execution, set the SYNCHRONIZED execution parameter
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @exe_id, @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1

-- Start the execution                                                         
EXEC [SSISDB].[catalog].[start_execution] @execution_id=@exe_id,@retry_count=0
                                          
-- Raise an error for unsuccessful package execution
-- Execution status values include the following:
-- created (1)
-- running (2)
-- canceled (3)
-- failed (4)
-- pending (5)
-- ended unexpectedly (6)
-- succeeded (7)
-- stopping (8)
-- completed (9) 
IF(SELECT [status]
   FROM [SSISDB].[catalog].[executions]
   WHERE execution_id=@exe_id)<>7
BEGIN
    SET @err_msg=N'Your package execution did not succeed for execution ID: ' + CAST(@exe_id AS NVARCHAR(20))
    RAISERROR(@err_msg,15,1)
END
GO
```

有关此脚本中代码的详细信息，请参阅[使用存储过程部署和执行 SSIS 包](../packages/deploy-integration-services-ssis-projects-and-packages.md#deploy-and-execute-ssis-packages-using-stored-procedures)。

## <a name="next-steps"></a>后续步骤
有关 SQL Server 代理的详细信息，请参阅 [包的 SQL Server 代理作业](../packages/sql-server-agent-jobs-for-packages.md)。

有关 SQL 数据库上的弹性作业的详细信息，请参阅[管理横向扩展的云数据库](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-overview)。
