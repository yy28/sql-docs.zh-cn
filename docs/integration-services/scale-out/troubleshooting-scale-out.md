---
title: "故障排除 SQL Server Integration Services (SSIS) 横向扩展 |Microsoft 文档"
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
ms.openlocfilehash: 41bb853dd08591596f6f5baa918e174d0c26a6b5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="troubleshooting-scale-out"></a>故障排除横向扩展

SSIS 的横向扩展涉及 communtication SSISDB，缩放出主服务和横向扩展辅助服务之间。 有时，通信将断开由于配置错误，缺少访问权限和其他原因。 本文档将帮助你解决你向外扩展的配置。

要进行调查你会遇到的现象，请按照以下逐个的步骤，直到问题得到解决。

### <a name="symptoms"></a>**症状** 
缩放出 Master 无法连接到 SSISDB 中。 

主属性无法在横向扩展管理器中显示。

主属性未填入 [SSISDB]。[目录]。[master_properties]

### <a name="solution"></a>**解决方案**
步骤 1： 检查向外扩展是否启用。

右键单击**SSISDB** SSMS 并检查的对象资源管理器中的节点**启用向外扩展功能**。

![向外扩展启用](media\isenabled.PNG)

如果属性值为 False，则启用横向扩展通过调用存储的过程 [SSISDB]。[目录]。[enable_scaleout]。

步骤 2： 检查出母版缩放配置文件中指定的 Sql Server 名称是否正确并重新启动缩放出主机服务。

### <a name="symptoms"></a>**症状** 
横向扩展辅助进程无法连接到缩放出主服务器

横向扩展辅助进程不会显示在扩展出管理器中添加它后

[SSISDB] 中未显示出工作人员缩放。[目录]。[worker_agents]

横向扩展辅助服务正在运行，横向扩展辅助处于脱机状态时

### <a name="solutions"></a>**解决方案** 
检查在横向扩展辅助服务日志中的错误消息\<驱动程序\>: \Users\\*[运行 worker 服务帐户]*\AppData\Local\SSIS\Cluster\Agent。

**用例** 

System.ServiceModel.EndpointNotFoundException： 没有终结点侦听时 https://*[MachineName]: [端口]*/ClusterManagement/ 无法接受消息。

步骤 1： 检查缩放出 Master 服务配置文件中指定的端口号是否正确并重新启动缩放出主机服务。 

步骤 2： 检查在横向扩展辅助服务配置中指定的主终结点是否正确并重新启动缩放出 Worker 服务。

步骤 3： 检查是否在缩放出主节点上打开防火墙端口。

步骤 4： 解决缩放出主节点和横向扩展辅助节点之间的任何其他连接问题。

**用例**

System.ServiceModel.Security.SecurityNegotiationException： 无法建立与机构的 SSL/TLS 安全通道的信任关系*[计算机名称]: [端口]*。 ---> System.Net.WebException： 基础连接已关闭： 未能建立 SSL/TLS 安全通道的信任关系。 ---> System.Security.Authentication.AuthenticationException： 远程证书为不符合验证过程。

步骤 1： 安装横向出 Master 到根证书存储在横向扩展辅助节点上的本地计算机的证书如果不是尚未安装和重新启动横向扩展辅助服务。

步骤 2： 检查主终结点中的主机名是否包括 Cn 的缩放出 Master 证书中。 如果没有，重置缩放出工作配置文件中的主终结点，并重新启动缩放出 Worker 服务。 

> [!Note]
> 如果不能更改由于 DNS 设置的主终结点的主机名，你必须更改缩放出主证书。 请参阅[处理中 SSIS 的横向扩展的证书](deal-with-certificates-in-ssis-scale-out.md)。

步骤 3： 检查在横向扩展辅助角色配置中指定的主指纹是否与缩放出主证书的指纹匹配。 

**用例**

System.ServiceModel.Security.SecurityNegotiationException： 无法建立安全通道的 SSL/TLS 与机构*[计算机名称]: [端口]*。 ---> System.Net.WebException： 该请求已中止： 无法创建 SSL/TLS 安全通道。

步骤 1： 检查运行缩放出 Worker 服务帐户是否具有访问横向扩展辅助证书通过以下命令。

```dos
winhttpcertcfg.exe -l -c LOCAL_MACHINE\MY -s {CN of the worker certificate}
```

如果帐户不具有访问权限，通过将以下命令来授予并重启缩放出 Worker 服务。

```dos
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the worker certificate} -a {the account running Scale Out Worker service}
```

**用例**

System.ServiceModel.Security.MessageSecurityException: HTTP 请求已禁止具有客户端身份验证方案匿名。 ---> System.Net.WebException： 远程服务器返回了错误: (403) 禁止访问。

步骤 1： 安装横向扩展辅助证书到缩放出主节点上的本地计算机的根证书存储否则尚未安装并重启横向扩展辅助服务。

步骤 2： 清理缩放出主节点上的本地计算机的根证书存储中的无用证书。

步骤 3： 配置 Schannel 以在 TLS/SSL 握手过程中，不再发送受信任的根证书颁发机构的列表，通过将下面的注册表项添加缩放出主节点上。

控制

值名称： SendTrustedIssuerList 

值类型： REG_DWORD 

值数据： 0 (False)

**用例**

System.ServiceModel.CommunicationException： 发出 HTTP 请求为 https:// 时发生错误*[计算机名称]: [端口]*  /ClusterManagement /。 这可能是因为，未使用 HTTP 正确配置服务器证书。在 HTTPS 的情况下的 SYS。 这也可能引起的客户端和服务器之间的安全绑定不匹配。 

步骤 1： 检查如果缩放出 Master 证书绑定到主终结点中的端口正确使用以下命令的主节点上。 检查显示的证书哈希将与的缩放出主证书指纹匹配。

```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```

如果绑定不正确，请使用以下命令将它重置并重新启动缩放出 Worker 服务。

```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={Master certificate thumbprint} certstorename=Root appid={random guid}
```

### <a name="symptoms"></a>**症状**
在向外扩展的执行不启动。

### <a name="solution"></a>**解决方案**

检查你所选的计算机 [SSISDB] 中运行包的状态。[目录]。[worker_agents]。 至少一个辅助必须联机且已启用。

### <a name="symptoms"></a>**症状** 
包成功运行，但不没有记录任何消息。

### <a name="solution"></a>**解决方案**

检查是否 SQL Server 身份验证允许通过 Sql Server 承载 SSISDB。

> [!Note]  
> 如果你已更改的帐户向外扩展日志记录，请参阅[缩放出日志记录更改的帐户](change-logdb-account.md)和验证连接字符串用于日志记录。

### <a name="symptoms"></a>**症状**
包执行报表中的错误消息是不够的故障排除。

### <a name="solution"></a>**解决方案**
可以在配置中 WorkerSettings.config TasksRootFolder 下找到详细的执行日志。 默认情况下，它是\<驱动程序\>: \Users\\*[帐户]*\AppData\Local\SSIS\ScaleOut\Tasks。 *[帐户]*是使用默认值 SSISScaleOutWorker140 运行缩放出 Worker 服务的帐户。

若要找到与包执行的日志*[执行 id]*，执行以下 T-SQL 命令，以获取*[任务 id]*。 然后，找到名为的子文件夹*[任务 id]*下 TasksRootFolder。<sup>1<sup>

```sql
SELECT [TaskId]
FROM [SSISDB].[internal].[tasks] tasks, [SSISDB].[internal].[executions] executions 
WHERE executions.execution_id = *Your Execution Id* AND tasks.JobId = executions.job_id
```
<sup>1</sup>此查询的故障排除目的仅和打开时横向扩展辅助进程的日志记录/诊断方案改进将来更改目标。 
