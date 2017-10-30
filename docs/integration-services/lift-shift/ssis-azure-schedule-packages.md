---
title: "计划在 Azure 上的 SSIS 包执行 |Microsoft 文档"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2f28400200105e8e63f787cbcda58c183ba00da5
ms.openlocfilehash: 2130e68d5e29671a2881d8762666cf852ff51259
ms.contentlocale: zh-cn
ms.lasthandoff: 10/18/2017

---
# <a name="schedule-the-execution-of-an-ssis-package-on-azure"></a>计划在 Azure 上的 SSIS 包的执行
你可以计划的执行的包存储在 SSISDB 目录数据库上的 Azure SQL 数据库服务器中通过选择以下的计划选项之一：
-   [SQL Server 代理](#agent)
-   [SQL 数据库弹性作业](#elastic)
-   [Azure 数据工厂 SQL Server 存储过程活动](#sproc)

## <a name="agent"></a>计划 SQL Server 代理的包

### <a name="prerequisite"></a>前提条件

你可以使用在本地 SQL Server 代理用于计划执行的 Azure SQL 数据库服务器上存储的包之前，必须将 SQL 数据库服务器添加为链接服务器。 有关详细信息，请参阅[创建链接服务器](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)和[链接服务器](../../relational-databases/linked-servers/linked-servers-database-engine.md)。

### <a name="create-a-sql-server-agent-job"></a>创建 SQL Server 代理作业

若要计划在本地 SQL Server 代理的包，创建一个作业具有作业步骤调用 SSIS 目录存储过程`[catalog].[create_execution]`然后`[catalog].[start_execution]`。 有关详细信息，请参阅[包的 SQL Server 代理作业](../packages/sql-server-agent-jobs-for-packages.md)。

1.  在 SQL Server Management Studio，连接到你要在其创建作业在本地 SQL Server 数据库。

2.  右键单击**SQL Server 代理**节点中，选择**新建**，然后选择**作业**以打开**新作业**对话框。

3.  在**新作业**对话框中，选择**步骤**页上，然后选择**新建**以打开**新建作业步骤**对话框。

4.  在**新建作业步骤**对话框中，选择`SSISDB`作为**数据库。**

5.  在命令字段中，输入类似于下面的示例所示的脚本的 Transact SQL 脚本：

    ```sql
    DECLARE @return_value int, @exe_id bigint 

    EXEC @return_value = [YourLinkedServer].[SSISDB].[catalog].[create_execution] 
    @folder_name=N'folderName', @project_name=N'projectName', 
    @package_name=N'packageName', @use32bitruntime=0, 
    @runinscaleout=1, @useanyworker=1, @execution_id=@exe_id OUTPUT 
 
    EXEC [YourLinkedServer].[SSISDB].[catalog].[start_execution] @execution_id=@exe_id

    GO
    ```

6.  完成配置和计划作业。

## <a name="elastic"></a>计划 SQL 数据库弹性作业的包

有关 SQL 数据库上的弹性作业的详细信息，请参阅[管理向外扩展的云数据库](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-overview)。

### <a name="prerequisites"></a>先决条件

你可以使用弹性作业计划的 Azure SQL 数据库服务器上的 SSISDB 目录数据库中存储的 SSIS 包之前，你必须执行以下操作：

1.  安装和配置弹性数据库作业组件。 有关详细信息，请参阅[安装弹性数据库作业概述](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-service-installation)。

2. 创建作业可用于将命令发送到 SSIS 目录数据库的数据库范围凭据。 有关详细信息，请参阅[CREATE DATABASE SCOPED CREDENTIAL (Transact SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)。

### <a name="create-an-elastic-job"></a>创建弹性作业

创建作业通过使用类似于下面的示例所示的脚本的 Transact SQL 脚本：

```sql
-- Create Elastic Jobs target group 
EXEC jobs.sp_add_target_group 'TargetGroup' 
? 
-- Add Elastic Jobs target group member 
EXEC jobs.sp_add_target_group_member @target_group_name='TargetGroup', 
    @target_type='SqlDatabase', @server_name='YourSQLDBServer.database.windows.net',
    @database_name='SSISDB' 
? 
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

## <a name="sproc"></a>计划 Azure 数据工厂 SQL Server 存储过程活动的包

> [!IMPORTANT]
> 使用下面的示例使用 Azure 数据工厂版本 1 中的 JSON 脚本存储过程活动。

若要计划的 Azure 数据工厂 SQL Server 存储过程活动的包，请执行以下操作：

1.  创建数据工厂。

2.  创建 SQL 数据库的链接的服务承载 SSISDB。

3.  创建驱动器计划的一个输出数据集。

4.  创建使用 SQL Server 存储过程活动来运行 SSIS 包的数据工厂管道。

本部分概述了这些步骤。 完整的数据工厂教程不在本文的范围。 有关详细信息，请参阅[SQL Server 存储过程活动](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-stored-proc-activity)。

### <a name="created-a-linked-service-for-the-sql-database-that-hosts-ssisdb"></a>创建承载 SSISDB 的 SQL 数据库的链接的服务
链接的服务，可以连接到 SSISDB 的数据工厂。

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

### <a name="create-an-output-dataset"></a>创建一个输出数据集
输出数据集包含的计划信息。

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
管道使用 SQL Server 存储过程活动来运行 SSIS 包。

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

你无需创建新的存储的过程来封装需创建并启动 SSIS 包执行的 TRANSACT-SQL 命令。 你可以作为值提供整个脚本`stmt`在前面的 JSON 示例的参数。 下面是示例脚本：

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

有关此脚本中的代码的详细信息，请参阅[部署和使用存储过程执行 SSIS 包](../packages/deploy-integration-services-ssis-projects-and-packages.md#deploy-and-execute-ssis-packages-using-stored-procedures)。

## <a name="next-steps"></a>后续步骤
有关 SQL Server 代理的详细信息，请参阅[包的 SQL Server 代理作业](../packages/sql-server-agent-jobs-for-packages.md)。

有关 SQL 数据库上的弹性作业的详细信息，请参阅[管理向外扩展的云数据库](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-overview)。

