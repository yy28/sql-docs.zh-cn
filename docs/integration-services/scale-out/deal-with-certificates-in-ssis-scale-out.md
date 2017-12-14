---
title: "处理 SQL Server Integration Services Scale Out 中的证书 | Microsoft Docs"
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
ms.openlocfilehash: e09fec1fcf9cf0221dad50d708adef773b297237
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="deal-with-certificates-in-sql-server-integration-services-scale-out"></a>处理 SQL Server Integration Services Scale Out 中的证书

若要保护 Scale Out Master 与 Scale Out Worker 之间的通信，需在 Scale Out 中使用两个证书，即 Scale Out Master 证书和 Scale Out Worker 证书。 

## <a name="scale-out-master-certificate"></a>Scale Out Master 证书

大多数情况下，Scale Out Master 证书在安装 Scale Out Master 的过程中配置。

在 SQL Server 安装向导的“Integration Services Scale Out 配置 - 主节点”页中，可以选择创建新的自签名 SSL 证书或使用现有 SSL 证书。

![主节点配置](media/master-config.PNG)

如果对证书没有特殊要求，可选择创建新的自签名 SSL 证书。 可在证书中进一步指定 CN。 请确保 CN 中包含 Scale Out Worker 稍后使用的主终结点的主机名。 默认包含主节点的计算机名称和 IP。 

如果选择使用现有证书，请单击“浏览...”，从本地计算机的**根**证书存储中选择 SSL 证书。

### <a name="change-scale-out-master-certificate"></a>更改 Scale Out Master 证书

由于证书过期或其他原因，可能需要更改 Scale Out Master 证书。 请执行下列步骤：

#### <a name="1-create-a-ssl-certificate"></a>1.创建 SSL 证书。
使用以下命令在主节点上创建并安装 SSL 证书：
```dos
MakeCert.exe -n CN={master endpoint host} SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```
例如：
```dos
MakeCert.exe -n CN=MasterMachine SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```

#### <a name="2-bind-the-certificate-to-master-port"></a>2.将证书绑定到主端口
使用以下命令检查原始绑定：
```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```
例如：
```dos
netsh http show sslcert ipport=0.0.0.0:8391
```
使用以下命令删除原始绑定并设置新绑定：
```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={SSL Certificate Thumbprint} certstorename=Root appid={original appid}
```
例如：
```dos
netsh http delete sslcert ipport=0.0.0.0:8391
netsh http add sslcert ipport=0.0.0.0:8391 certhash=01d207b300ca662f479beb884efe6ce328f77d53 certstorename=Root appid={a1f96506-93e0-4c91-9171-05a2f6739e13}
```
#### <a name="3-update-scale-out-master-service-configuration-file"></a>3.更新 Scale Out Master 服务配置文件
更新主节点上的 Scale Out Master 服务配置文件 \<驱动程序\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config。 将 **SSLCertThumbprint** 更新为新 SSL 证书的指纹。

#### <a name="4-restart-scale-out-master-service"></a>4.重启 Scale Out Master 服务

#### <a name="5-reconnect-scale-out-worker-to-scale-out-master"></a>5.将 Scale Out Worker 重新连接到 Scale Out Master
对于每个 Scale Out Worker，均使用 [Scale Out Manager](integration-services-ssis-scale-out-manager.md) 删除并重新添加 Worker 或执行下面的步骤 5.1 至 5.3：

5.1 将客户端 SSL 证书安装到辅助节点上本地计算机的根存储

5.2 更新辅助节点上的 Scale Out Worker 服务配置文件 \<驱动程序\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config。 将 **MasterHttpsCertThumbprint** 更新为新 SSL 证书的指纹。

5.3 重启 Scale Out Worker 服务


## <a name="scale-out-worker-certificate"></a>Scale Out Worker 证书

Scale Out Worker 证书在安装 Scale Out Worker 的过程中自动生成。 

### <a name="change-scale-out-worker-certificate"></a>更改 Scale Out Worker 证书

若要更改 Scale Out Worker 证书，请按照以下步骤操作。

#### <a name="1-create-a-certificate"></a>1.创建证书
使用以下命令创建并安装证书：
```dos
MakeCert.exe -n CN={worker machine name};CN={worker machine ip} SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
例如：
```dos
MakeCert.exe -n CN=WorkerMachine;CN=10.0.2.8 SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
#### <a name="2-install-the-client-certificate-to-the-root-store-of-local-machine-on-worker-node"></a>2.将客户端证书安装到辅助节点上本地计算机的根存储

#### <a name="3-give-service-access-to-the-certificate"></a>3.为证书提供服务访问权限
删除旧证书，并使用以下命令为新证书提供 Scale Out Worker 服务访问权限：
```dos
certmgr.exe /del /c /s /r localmachine My /n {CN of the old certificate}
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the new certificate} -a {the account running Scale Out Worker service}
```
例如：
```dos
certmgr.exe /del /c /s /r localmachine My /n WorkerMachine
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s WorkerMachine -a SSISScaleOutWorker140
```
#### <a name="4-update-scale-out-worker-configuration-file"></a>4.更新 Scale Out Worker 配置文件
更新辅助节点上的 Scale Out Worker 服务配置文件 \<驱动程序\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config。 将 **WorkerHttpsCertThumbprint** 更新为新证书的指纹。

#### <a name="5-install-the-client-certificate-to-the-root-store-of-local-machine-on-master-node"></a>5.将客户端证书安装到主节点上本地计算机的根存储

#### <a name="6-restart-scale-out-worker-service"></a>6.重启 Scale Out Worker 服务
