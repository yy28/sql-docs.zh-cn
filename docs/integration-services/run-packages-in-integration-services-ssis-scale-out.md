---
title: "在 Integration Services (SSIS) Scale Out 中运行包 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4c2f4cd7-9c47-416d-bb1e-40acc3e05342
caps.latest.revision: 5
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 5
---
# 在 Integration Services (SSIS) Scale Out 中运行包
包部署到 Integration Services 服务器后，可在 Scale Out 中执行包。

## <a name="run-packages-with-execute-package-in-scale-out-dialog"></a>通过“在 Scale Out 中执行包”对话框运行包 

1. ### <a name="open-the-execute-package-in-scale-out-dialog-box"></a>打开“在 Scale Out 中执行包”对话框 ###
    在 [!INCLUDE[ssManStudioFull_md](../includes/ssmanstudiofull-md.md)] 中，连接到 Integration Services 服务器。 在对象资源管理器中，展开树，显示“Integration Services 目录”下的节点。 右键单击 **SSISDB** 节点或者要运行的项目或包，然后单击“在 Scale Out 中执行”。
2. ### <a name="select-packages-and-set-the-options"></a>选择包并设置选项 ###
    在“包选择”页中，选择要运行的多个包并设置每个包的环境、参数、连接管理器和高级选项。 单击包以设置这些选项。
    
    在“高级”选项卡中，设置名为“重试计数”的 Scale Out 选项。 该选项设置包执行失败后将重试的次数。
3. ### <a name="select-machines"></a>选择计算机 ###
    在“计算机选择”页上，选择运行包的 Scale Out Worker 计算机。 默认情况下，允许任何计算机运行包。 

   > [!NOTE]
> 使用 Scale Out Worker 服务的用户帐户的凭据执行包，该服务显示在“计算机选择”页上。 默认情况下，该帐户是 NT Service\SSISScaleOutWorker140。 可能需要更改为自己的实验室帐户。

4. ### <a name="run-the-packages-and-view-reports"></a>运行包和查看报表 
    单击“确定”，启动包执行。 若要查看包执行报表，在对象资源管理器中右键单击包，单击“报表”，单击“所有执行”，查找该执行。
    
    
## <a name="run-packages-with-stored-procedures"></a>在存储过程中运行包

1. ### <a name="create-executions"></a>创建执行 ###
    对每个包调用 [catalog].[create_execution]。 将参数 **@runincluster** 设置为 True。 如果不允许所有的 Scale Out Worker 计算机运行包，请将参数 **@useanyworker** 设置为 False。   
2. ### <a name="set-execution-parameters"></a>设置执行参数 ###
    对每个执行调用 [catalog].[set_execution_parameter_value]。
3. ### <a name="set-scale-out-workers"></a>设置 Scale Out Worker ###
    调用 [catalog].[add_execution_worker]。 如果允许任何计算机运行包，则无需调用此存储过程。 
4. ### <a name="start-executions"></a>启动执行 ###
    调用 [catalog].[start_execution]。 设置参数 **@retry_count**，设置包执行失败后将重试的次数。
    
    ### <a name="example"></a>示例  ###  
    以下示例使用一个 Scale Out Worker 在 Scale Out 中运行两个包，package1.dtsx 和 package2.dtsx。  
    ```
    Declare @execution_id bigint
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder1', @project_name=N'project1', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runincluster=True
    Select @execution_id
    DECLARE @var0 smallint = 1
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
    EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
    EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
    GO

    Declare @execution_id bigint
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package2.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder2', @project_name=N'project2', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runincluster=True
    Select @execution_id
    DECLARE @var0 smallint = 1
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
    EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
    EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
    GO
    ```


## <a name="permissions"></a>Permissions
在 Scale Out 中运行包需要以下权限之一：

-   **ssis_admin** 数据库角色中的成员资格  

-   **ssis_cluster_executor** 数据库角色中的成员资格  
  
-   **sysadmin** 服务器角色中的成员资格  
    