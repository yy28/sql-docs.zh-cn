---
title: "Integration Services (SSIS) Scale Out Master | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2e89803f-0471-40ba-b5e4-ddd2c815eecd
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Integration Services (SSIS) Scale Out Master
Scale Out Master 通过 SSISDB 目录和 Scale Out Master 服务来管理 Scale Out 系统。 

SSISDB 目录可存储 Scale Out Worker、包和执行的所有信息。 它可提供接口，以便在 Scale Out 中启用 Scale Out Worker 和执行包。 有关详细信息，请参阅[演练：设置 Integration Services Scale Out](../integration-services/walkthrough-set-up-integration-services-scale-out.md)、[在 Integration Services 中运行包](../integration-services/run-packages-in-integration-services-ssis-scale-out.md)。

Scale Out Master 服务是一项 Windows 服务，负责与 Scale Out Worker 的通信。 它可通过 HTTPS 与 Scale Out Worker 交换包执行的状态，并对 SSISDB 中的数据进行操作。 

## <a name="scale-out-related-sql-views-and-stored-procdures-in-ssisdb"></a>SSISDB 中与 Scale Out 相关的 SQL 视图和存储过程

### <a name="views"></a>Views:
[[catalog].[master_properties]](../integration-services/system-views/catalog-master-properties-ssisdb-database.md)、[[catalog].[worker_agents]](../integration-services/system-views/catalog-worker-agents-ssisdb-database.md)。
### <a name="stored-procedures"></a>存储过程：

- 有关 Scale Out Worker 管理：  
 [[catalog].[disable_worker_agent]](../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md)、[[catalog].[enable_worker_agent]](../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md)。
- 有关在 Scale Out 中执行包：   
[[catalog].[create_execution]](../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)、[[catalog].[add_execution_worker]](../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)、[[catalog].[start_execution]](../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)。   

## <a name="configure-sql-server-integration-services-scale-out-master-service"></a>配置 SQL Server Integration Services Scale Out Master 服务
可使用 \<driver\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config 文件配置 Scale Out Master 服务。 更新配置文件之后，必须重启服务。


配置  |Description  |“默认值”  
---------|---------|---------
PortNumber|用于与 Scale Out Worker 进行通信的网络端口号。|8391         
SSLCertThumbprint|用于保护与 Scale Out Worker 之间通信的 SSL 证书的指纹。|SSL 证书的指纹在 Scale Out Master 安装期间指定         
InstanceName|包含 SSISDB 目录的 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 实例的名称。 MSSQLSERVER 是默认 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 实例的名称。 |与 Scale Out Master 一起安装的 SQL Server 实例的名称         
CleanupCompletedJobsIntervalInMs|清理已完成的执行作业的间隔时间（以毫秒为单位）。|43200000         
DealWithExpiredTasksIntervalInMs|处理过期的执行作业的间隔时间（以毫秒为单位）。|300000
MasterHeartbeatIntervalInMs|Scale Out Master 检测信号的间隔时间（以毫秒为单位）。 这将指定 Scale Out Master 更新其在 SSISDB 目录中联机状态的间隔时间。|30000        

## <a name="view-scale-out-master-service-log"></a>查看 Scale Out Master 服务日志
Scale Out Master 服务日志文件位于 \<driver\>:\Users\\*[account]*\AppData\Local\SSIS\Cluster\Master 文件夹路径中。 

*[account]* 文件夹指运行 Scale Out Master 服务的帐户。 默认情况下，该帐户为 SSISScaleOutMaster140。