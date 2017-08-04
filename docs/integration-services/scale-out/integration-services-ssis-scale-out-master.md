---
title: "SQL Server Integration Services (SSIS) 横向扩展 Master |Microsoft 文档"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1672c015186998065b5d6dc95897147aa11d14ec
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-ssis-scale-out-master"></a>Integration Services (SSIS) Scale Out Master
Scale Out Master 通过 SSISDB 目录和 Scale Out Master 服务来管理 Scale Out 系统。 

SSISDB 目录可存储 Scale Out Worker、包和执行的所有信息。 它可提供接口，以便在 Scale Out 中启用 Scale Out Worker 和执行包。 有关详细信息，请参阅[演练：设置 Integration Services Scale Out](walkthrough-set-up-integration-services-scale-out.md)、[在 Integration Services 中运行包](run-packages-in-integration-services-ssis-scale-out.md)。

Scale Out Master 服务是一项 Windows 服务，负责与 Scale Out Worker 的通信。 它可通过 HTTPS 与 Scale Out Worker 交换包执行的状态，并对 SSISDB 中的数据进行操作。 

## <a name="scale-out-related-sql-views-and-stored-procedures-in-ssisdb"></a>向外扩展相关 SQL 视图和存储过程在 SSISDB

#### <a name="views"></a>Views:
[[catalog].[master_properties]](../../integration-services/system-views/catalog-master-properties-ssisdb-database.md)、[[catalog].[worker_agents]](../../integration-services/system-views/catalog-worker-agents-ssisdb-database.md)。

#### <a name="stored-procedures"></a>存储过程：

- 有关 Scale Out Worker 管理：  
 [[catalog].[disable_worker_agent]](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md)、[[catalog].[enable_worker_agent]](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md)。
- 有关在 Scale Out 中执行包：   
[[catalog].[create_execution]](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)、[[catalog].[add_execution_worker]](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)、[[catalog].[start_execution]](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)。   

## <a name="configure-sql-server-integration-services-scale-out-master-service"></a>配置 SQL Server Integration Services Scale Out Master 服务
可使用 \<driver\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config 文件配置 Scale Out Master 服务。 更新配置文件之后，必须重启服务。


配置  |Description  |“默认值”  
---------|---------|---------
PortNumber|用于与 Scale Out Worker 进行通信的网络端口号。|8391         
SSLCertThumbprint|用于保护与 Scale Out Worker 之间通信的 SSL 证书的指纹。|SSL 证书的指纹在 Scale Out Master 安装期间指定         
SqlServerName|名称[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]包含 SSISDB 目录。 例如 ServerName\\\\InstanceName。|随缩放出 Master 一起安装的 SQL server 名称。         
CleanupCompletedJobsIntervalInMs|清理已完成的执行作业的间隔时间（以毫秒为单位）。|43200000         
DealWithExpiredTasksIntervalInMs|处理过期的执行作业的间隔时间（以毫秒为单位）。|300000
MasterHeartbeatIntervalInMs|Scale Out Master 检测信号的间隔时间（以毫秒为单位）。 这将指定 Scale Out Master 更新其在 SSISDB 目录中联机状态的间隔时间。|30000
SqlConnectionTimeoutInSecs|以秒为单位的 SQL 连接超时值时连接到 SSISDB。|15        

## <a name="view-scale-out-master-service-log"></a>查看 Scale Out Master 服务日志
缩放出主服务日志文件位于\<驱动程序\>: \Users\\*[帐户]*\AppData\Local\SSIS\ScaleOut\Master 文件夹路径。 

*[帐户]*指运行缩放出主服务的帐户。 默认情况下，该帐户为 SSISScaleOutMaster140。

