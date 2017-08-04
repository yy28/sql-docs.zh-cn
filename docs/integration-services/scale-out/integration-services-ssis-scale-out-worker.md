---
title: "SQL Server Integration Services (SSIS) 横向扩展辅助 |Microsoft 文档"
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
ms.openlocfilehash: 77cf90268938bada458aa159a5f18f885491b407
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-ssis-scale-out-worker"></a>Integration Services (SSIS) Scale Out Worker

横向扩展辅助进程运行[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)]缩放出 Worker 服务请求执行缩放出母版的任务，并执行本地具有 ISServerExec.exe 的程序包。

## <a name="configure-sql-server-integration-services-scale-out-worker-service"></a>配置 SQL Server Integration Services Scale Out Worker 服务
可使用 \<driver\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config 文件配置 Scale Out Worker 服务。 更新配置文件之后，必须重启服务。

配置  |Description  |默认值  
---------|---------|---------
DisplayName|Scale Out Worker 的显示名称。 **在不使用在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]自 2017 年。**|计算机名称         
Description|Scale Out Worker 的说明。 **在不使用在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]自 2017 年。**|Empty         
MasterEndpoint|连接到 Scale Out Master 的终结点。|该终结点在 Scale Out Worker 安装期间设置         
MasterHttpsCertThumbprint|用于对 Scale Out Master 进行身份验证的客户端 SSL 证书的指纹|客户端证书的指纹在 Scale Out Worker 安装期间指定。          
WorkerHttpsCertThumbprint|用于对 Scale Out Worker 进行身份验证的 Scale Out Master 证书的指纹。|证书的指纹在 Scale Out Worker 安装期间自动创建并安装          
StoreLocation|Worker 证书的存储位置。|LocalMachine       
StoreName|Worker 证书所在位置的存储名称。|My         
AgentHeartbeatInterval|Scale Out Worker 检测信号的间隔时间。|00:01:00         
TaskHeartbeatInterval|Scale Out Worker 报告任务状态的间隔时间。|00:00:10         
HeartbeatErrorTollerance|上一次任务检测信号成功后，如果接收到检测信号的错误响应，任务将终止。|00:10:00      
TaskRequestMaxCPU|Scale Out Worker 请求任务的 CPU 上限。 **在不使用在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]自 2017 年。**|70.0         
TaskRequestMinMemory|Scale Out Worker 请求任务的内存（以 MB 表示）下限。 **在不使用在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]自 2017 年。**|100.0         
MaxTaskCount|Scale Out Worker 可保留的最大任务数。|10         
LeaseInternval|Scale Out Worker 可保留任务的租用间隔。|00:01:00         
TasksRootFolder|任务日志的文件夹。 如果该值为空，则使用 \<driver\>:\Users\\*[account]*\AppData\Local\SSIS\Cluster\Tasks 文件夹路径。 [account] 是运行 Scale Out Worker 服务的帐户。 默认情况下，该帐户为 SSISScaleOutWorker140。|Empty         
TaskLogLevel|Scale Out Worker 的任务日志级别。 (Verbose 0x01, Information 0x02, Warning 0x04, Error 0x08, Progress 0x10, CriticalError 0x20, Audit 0x40)|126 (Information,Warning,Error,Progress,CriticalError,Audit)     
TaskLogSegment|任务日志文件的时间跨度。|00:00:00         
TaskLogEnabled|指定是否启用任务日志。|true         
ExecutionLogCacheFolder|用于缓存包执行日志的文件夹。 如果该值为空，则使用 \<driver\>:\Users\\*[account]*\AppData\Local\SSIS\Cluster\Agent\ELogCache 文件夹路径。 [account] 是运行 Scale Out Worker 服务的帐户。 默认情况下，该帐户为 SSISScaleOutWorker140。|Empty         
ExecutionLogMaxBufferLogCount|在内存的一个执行日志缓冲区中，缓存的执行日志的最大数量。|10000        
ExecutionLogMaxInMemoryBufferCount|用于执行日志的内存中，执行日志缓冲区的最大数量。|10         
ExecutionLogRetryCount|执行日志记录失败时的重试次数。|3
ExecutionLogRetryTimeout|如果执行日志记录失败重试超时。 如果达到 ExecutionLogRetryTimeout，则忽略 ExecutionLogRetryCount。|7.00:00:00 （7 天）        
AgentId|Scale Out Worker 的 Worker 代理 ID|自动生成        

## <a name="view-scale-out-worker-log"></a>查看 Scale Out Worker 日志
横向扩展辅助服务的日志文件处于\<驱动程序\>: \Users\\*[帐户]*\AppData\Local\SSIS\ScaleOut\Agent 文件夹路径。

每项任务的日志位置由 TasksRootFolder 在 WorkerSettings.config 文件中进行配置。 如果未指定，日志将处于\<驱动程序\>: \Users\\*[帐户]*\AppData\Local\SSIS\ScaleOut\Tasks 文件夹路径。 

*[帐户]*是运行缩放出 Worker 服务的帐户。 默认情况下，该帐户为 SSISScaleOutWorker140。
