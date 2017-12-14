---
title: "SQL Server Integration Services (SSIS) Scale Out 故障排除 | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 56d61bc6ba76514ba2291243002a7423ec8e265c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="troubleshooting-scale-out"></a>Scale Out 故障排除

SSIS Scale Out 涉及 SSISDB、Scale Out Master 服务和 Scale Out Worker 服务之间的通信。 有时，通信会因配置错误、缺少访问权限及其他原因而中断。 可借助本文档排查 Scale Out 配置的问题。

要调查出现的问题，请按照下面的步骤逐一操作，直到解决问题。

### <a name="symptoms"></a>**现象** 
Scale Out Master 无法连接 SSISDB。 

Scale Out Manager 中无法显示主控形状属性。

主控形状属性未填入 [SSISDB].[catalog].[master_properties]

### <a name="solution"></a>**解决方案**
步骤 1：检查是否已启用 Scale Out。

右键单击 SSMS 对象资源管理器中的“SSISDB”节点，然后选中“启用 Scale Out 功能”。

![是否已启用 Scale Out](media\isenabled.PNG)

如果属性值为 False，通过调用存储过程 [SSISDB].[catalog].[enable_scaleout] 启用 Scale Out。

步骤 2：检查 Scale Out Master 配置文件中指定的 SQL Server 名称是否正确并重启 Scale Out Master 服务。

### <a name="symptoms"></a>**现象** 
Scale Out Worker 无法连接 Scale Out Master

Scale Out Worker 在添加到 Scale Out Manager 中后无法显示

Scale Out Worker 在 [SSISDB].[catalog].[worker_agents] 中不显示

Scale Out Worker 服务处于运行状态，而 Scale Out Worker 处于脱机状态

### <a name="solutions"></a>**解决方案** 
在 \<driver\>:\Users\\[account running worker service]\AppData\Local\SSIS\Cluster\Agent 目录下查看 Scale Out Worker 服务日志中的错误消息。

**事例** 

System.ServiceModel.EndpointNotFoundException：可接受消息的 https://[MachineName]:[Port]/ClusterManagement/ 下无任何终结点侦听。

步骤 1：检查 Scale Out Master 配置文件中指定的端口号是否正确并重启 Scale Out Master 服务。 

步骤 2：检查 Scale Out Master 服务配置中指定的主终结点是否正确并重启 Scale Out Worker 服务。

步骤 3：检查 Scale Out Mater 节点上的防火墙端口是否开启。

步骤 4：解决 Scale Out Master 节点和 Scale Out Worker 节点之间任何其他的连接问题。

**事例**

System.ServiceModel.Security.SecurityNegotiationException：无法使用授权“[Machine Name]:[Port]”为 SSL/TLS 安全通道建立信任关系。 ---> System.Net.WebException：基础连接已关闭：无法为 SSL/TLS 安全通道建立信任关系。 ---> System.Security.Authentication.AuthenticationException：根据验证流程，远程证书无效。

步骤 1：如果尚未安装 Scale Out Master 证书，请将其安装到 Scale Out Worker 节点上的本地计算机的根证书存储中并重启 Scale Out Worker 服务。

步骤 2：检查主终结点的主机名是否包含在 Scale Out Master 证书的 CN 中。 如果没有，重置 Scale Out Worker 配置文件中的主终结点并重启 Scale Out Worker 服务。 

> [!Note]
> 如果因 DNS 设置不能更改主终结点的主机名，则必须更改 Scale Out Master 证书。 请参阅[处理SSIS Scale Out 中的证书](deal-with-certificates-in-ssis-scale-out.md)。

步骤 3：检查 Scale Out Worker 配置中指定的主指纹是否匹配 Scale Out Master 证书的指纹。 

**事例**

System.ServiceModel.Security.SecurityNegotiationException：无法使用授权“[Machine Name]:[Port]”为 SSL/TLS 建立安全通道。 ---> System.Net.WebException：请求已中止：无法创建 SSL/TLS 安全通道。

步骤 1：通过使用下面的命令，检查运行 Scale Out Worker 服务的帐户是否有权访问 Scale Out Worker 证书。

```dos
winhttpcertcfg.exe -l -c LOCAL_MACHINE\MY -s {CN of the worker certificate}
```

如果帐户无权访问，通过下面的命令授予权限并重启 Scale Out Worker 服务。

```dos
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the worker certificate} -a {the account running Scale Out Worker service}
```

**事例**

System.ServiceModel.Security.MessageSecurityException：HTTP 请求已被禁止，同时客户端身份验证方案为“匿名”。 ---> System.Net.WebException：远程服务器返回错误：(403) 禁止访问。

步骤 1：如果尚未安装 Scale Out Worker 证书，请将其安装到 Scale Out Master 节点上的本地计算机的根证书存储中并重启 Scale Out Worker 服务。

步骤 2：清理 Scale Out Master 上本地计算机根证书存储中的无用证书。

步骤 3：将 Schannel 配置为在 TLS/SSL 握手过程中不再发送受信任的根证书颁发机构列表，方法是在 Scale Out Master 节点上添加以下注册表项。

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

值名称：SendTrustedIssuerList 

值类型：REG_DWORD 

值数据：0 (False)

**事例**

System.ServiceModel.CommunicationException：向 https://[Machine Name]:[Port]/ClusterManagement/ 发出 HTTP 请求时出错。 这可能是因为未正确使用 HTTP.SYS 在 HTTPS 事例中配置服务器证书。 此外，客户端与服务器之间的安全绑定不匹配，也可能造成该异常。 

步骤 1：使用下面的命令，检查 Scale Out Master 证书是否已正确绑定到主节点上主终结点中的端口。 检查显示的证书哈希与 Scale Out Master 证书指纹是否匹配。

```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```

如果绑定不正确，使用下面的命令进行重置并重启 Scale Out Worker 服务。

```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={Master certificate thumbprint} certstorename=Root appid={random guid}
```

### <a name="symptoms"></a>**现象**
在 Scale Out Manager 中，Scale Out Worker 连接到 Scale Out Master 时验证失败，并收到错误消息：“无法打开计算机上的证书存储”。

### <a name="solution"></a>**解决方案**

步骤 1：以管理员身份运行 Scale Out Manager。 如果使用 SSMS 打开它，需要以管理员身份运行 SSMS。

步骤 2：如果远程注册表服务未运行，在计算机上启动它。

### <a name="symptoms"></a>**现象**
Scale Out 中“执行”不启动。

### <a name="solution"></a>**解决方案**

检查选来运行 [SSISDB].[catalog].[worker_agents] 中包的计算机的状态。 必须至少联机启动一个辅助角色。

### <a name="symptoms"></a>**现象** 
包运行成功，但未记录任何消息。

### <a name="solution"></a>**解决方案**

检查 SQL Server 承载 SSISDB 是否允许 SQL Server 身份验证。

> [!Note]  
> 如果已更改用于 Scale Out 日志记录的帐户，请参阅[更改用于 Scale Out 日志记录的帐户](change-logdb-account.md)并验证用于日志记录的连接字符串。

### <a name="symptoms"></a>**现象**
包执行报告中的错误消息不充足，无法进行故障排除。

### <a name="solution"></a>**解决方案**
可在 WorkerSettings.config 中配置的 TasksRootFolder 下找到更多执行日志。默认情况下，路径为 \<driver\>:\Users\\[account]\AppData\Local\SSIS\ScaleOut\Tasks。 [account] 是运行 Scale Out Worker 服务的帐户，其默认值为 SSISScaleOutWorker140。

若要为执行 ID 为 [execution id] 的包查找日志，请执行下面的 T-SQL 命令，获取 [task id]（任务 ID）。 然后，在 TasksRootFolder.<sup>1<sup> 下查找名称为 [task id] 的子文件夹

```sql
SELECT [TaskId]
FROM [SSISDB].[internal].[tasks] tasks, [SSISDB].[internal].[executions] executions 
WHERE executions.execution_id = *Your Execution Id* AND tasks.JobId = executions.job_id
```
<sup>1</sup> 本查询仅用于故障排除，会随 Scale Out Worker 的日志记录/诊断方案的改进而发生更改。 
