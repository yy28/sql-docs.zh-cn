---
title: "SQL Server Integration Services (SSIS) 中的运行的包向外扩展 |Microsoft 文档"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
f1_keywords:
- sql13.ssis.ssms.ispackageexecuteinscaleout.f1
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2c158ae6a711ecb5f5065561c0c8c303e9a09980
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---

# <a name="run-packages-in-integration-services-ssis-scale-out"></a>在 Integration Services (SSIS) 的横向扩展运行包
包部署到 Integration Services 服务器后，可在 Scale Out 中执行包。

## <a name="run-packages-with-execute-package-in-scale-out-dialog"></a>使用执行包中向外扩展对话框运行包 

1. 打开“在 Scale Out 中执行包”对话框

    在 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 中，连接到 Integration Services 服务器。 在对象资源管理器中，展开树，显示“Integration Services 目录” 下的节点。 右键单击 **SSISDB** 节点或者要运行的项目或包，然后单击“在 Scale Out 中执行” 。

2. 选择包并设置选项

    在“包选择”  页中，选择要运行的多个包并设置每个包的环境、参数、连接管理器和高级选项。 单击包以设置这些选项。
    
    在“高级”  选项卡中，设置名为“重试计数” 的 Scale Out 选项。 该选项设置包执行失败后将重试的次数。

    > [!Note]
    > **出错时转储**选项时运行缩放出 Worker 服务的帐户是本地计算机的管理员才能起作用。

3. 选择计算机

    在“计算机选择”  页上，选择运行包的 Scale Out Worker 计算机。 默认情况下，允许任何计算机运行包。 

   > [!Note] 
   > 使用 Scale Out Worker 服务的用户帐户的凭据执行包，该服务显示在“计算机选择”  页上。 默认情况下，该帐户是 NT Service\SSISScaleOutWorker140。 可能需要更改为自己的实验室帐户。

   >[!WARNING]
   >由同一个辅助角色上的不同用户触发的包执行将在使用同一帐户运行。 在它们之间没有安全边界。 

4. 运行包和查看报表 

    单击“确定”  ，启动包执行。 若要查看包执行报表，在对象资源管理器中右键单击包，单击“报表” ，单击“所有执行” ，查找该执行。
    
## <a name="run-packages-with-stored-procedures"></a>在存储过程中运行包

1. 创建执行

    对每个包调用 [catalog].[create_execution]。 将参数 **@runinscaleout** 设置为 True。 如果不允许所有的 Scale Out Worker 计算机运行包，请将参数 **@useanyworker** 设置为 False。   

2. 设置执行参数

    对每个执行调用 [catalog].[set_execution_parameter_value]。

3. 设置 Scale Out Worker

    调用 [catalog].[add_execution_worker]。 如果允许任何计算机运行包，则无需调用此存储过程。 

4. 启动执行

    调用 [catalog].[start_execution]。 设置参数 **@retry_count** ，设置包执行失败后将重试的次数。
    
#### <a name="example"></a>示例
以下示例使用一个 Scale Out Worker 在 Scale Out 中运行两个包，package1.dtsx 和 package2.dtsx。  

```sql
Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder1', @project_name=N'project1', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runinscaleout=True
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
GO

Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package2.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder2', @project_name=N'project2', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runinscaleout=True
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
GO
```

### <a name="permissions"></a>Permissions
在 Scale Out 中运行包需要以下权限之一：

-   **ssis_admin** 数据库角色中的成员资格  

-   **ssis_cluster_executor** 数据库角色中的成员资格  
  
-   **sysadmin** 服务器角色中的成员资格  

## <a name="set-default-execution-mode"></a>设置默认执行模式
若要设置默认执行模式为"横向扩展"，右键单击**SSISDB** SSMS 并选择的对象资源管理器中的节点**属性**。
在**目录属性**对话框中，将**服务器范围内默认的执行模式**到**向外扩展**。

在此设置后，没有无需指定 **@runinscaleout**  [目录] 的参数。 [create_execution]。 执行在中执行的向外扩展自动。 

![Exe 模式](media\exe-mode.PNG)

若要切换回非-向外扩展模式的默认执行模式下，只需设置**服务器范围内默认的执行模式**到**服务器**。

## <a name="run-package-in-sql-agent-job"></a>在 SQL 代理作业中运行包
在 Sql 代理作业中，你可以选择一个步骤的作业以运行 SSIS 包。 若要运行包中向外扩展，你可以利用更高版本的默认执行模式。 设置默认执行模式为"横向扩展"后, 将在向外扩展中运行 Sql 代理作业中的包。

