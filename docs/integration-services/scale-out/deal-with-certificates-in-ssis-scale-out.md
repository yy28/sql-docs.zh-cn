---
title: 管理 SQL Server Integration Services Scale Out 的证书 | Microsoft Docs
ms.custom: This article describes how to manage certificates to secure communications between SSIS Scale Out Master and Scale Out Workers.
ms.date: 12/19/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: scale-out
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: craigg
ms.openlocfilehash: 08834fab42c8c74f730a0d9602c1ddb71c76bab6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="manage-certificates-for-sql-server-integration-services-scale-out"></a>管理 SQL Server Integration Services Scale Out 的证书

为保护 Scale Out Master 与 Scale Out Worker 之间的通信，SSIS Scale Out 使用了两个证书 - 一个用于 Master，另一个用于 Worker。 

## <a name="scale-out-master-certificate"></a>Scale Out Master 证书

大多数情况下，Scale Out Master 证书在安装 Scale Out Master 的过程中配置。

在 SQL Server 安装向导的“Integration Services Scale Out 配置 - 主节点”页中，可以选择创建新的自签名 SSL 证书或使用现有 SSL 证书。

![主节点配置](media/master-config.PNG)

**新证书**。 如果对证书没有特殊要求，可选择创建新的自签名 SSL 证书。 可在证书中进一步指定 CN。 请确保 CN 中包含 Scale Out Worker 稍后使用的主终结点的主机名。 默认情况下，计算机名和主节点的 IP 地址也包含在内。 

**现有证书**。 如果选择使用现有证书，请单击“浏览”，从本地计算机的根证书存储中选择 SSL 证书。

### <a name="change-the-scale-out-master-certificate"></a>更改 Scale Out Master 证书

由于证书过期或其他原因，可能需要更改 Scale Out Master 证书。 要更改 Scale Out Master 证书，请执行以下操作：

#### <a name="1-create-an-ssl-certificate"></a>1.创建 SSL 证书。
使用以下命令在主节点上创建并安装新 SSL 证书：

```dos
MakeCert.exe -n CN={master endpoint host} SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```
例如：

```dos
MakeCert.exe -n CN=MasterMachine SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```

#### <a name="2-bind-the-certificate-to-the-master-port"></a>2.将证书绑定到主端口
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

#### <a name="3-update-the-scale-out-master-service-configuration-file"></a>3.更新 Scale Out Master 服务配置文件
在主节点上更新 Scale Out Master 服务配置文件 `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config`。 将 **SSLCertThumbprint** 更新为新 SSL 证书的指纹。

#### <a name="4-restart-the-scale-out-master-service"></a>4.重启 Scale Out Master 服务

#### <a name="5-reconnect-scale-out-workers-to-scale-out-master"></a>5.将 Scale Out Worker 重新连接到 Scale Out Master
对于每个 Scale Out Worker，均使用 [Scale Out Manager](integration-services-ssis-scale-out-manager.md) 删除并重新添加 Worker，或执行以下操作：

A.  将客户端 SSL 证书安装到辅助节点上本地计算机的根存储。

B.  更新 Scale Out Worker 服务配置文件。

    Update the Scale Out Worker service configuration file, `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config`, on the Worker node. Update **MasterHttpsCertThumbprint** to the thumbprint of the new SSL certificate.

c.  重启 Scale Out Worker 服务。

## <a name="scale-out-worker-certificate"></a>Scale Out Worker 证书

Scale Out Worker 证书在安装 Scale Out Worker 的过程中自动生成。 

### <a name="change-the-scale-out-worker-certificate"></a>更改 Scale Out Worker 证书

要更改 Scale Out Worker 证书，请执行以下操作：

#### <a name="1-create-a-certificate"></a>1.创建证书
使用以下命令创建并安装证书：

```dos
MakeCert.exe -n CN={worker machine name};CN={worker machine ip} SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```

例如：

```dos
MakeCert.exe -n CN=WorkerMachine;CN=10.0.2.8 SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```

#### <a name="2-install-the-client-certificate-to-the-root-store-of-the-local-computer-on-the-worker-node"></a>2.将客户端证书安装到辅助节点上本地计算机的根存储

#### <a name="3-grant-service-access-to-the-certificate"></a>3.为证书提供服务访问权限
删除旧证书，并使用以下命令为新证书授予 Scale Out Worker 服务访问权限：

```dos
certmgr.exe /del /c /s /r localmachine My /n {CN of the old certificate}
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the new certificate} -a {the account running Scale Out Worker service}
```

例如：

```dos
certmgr.exe /del /c /s /r localmachine My /n WorkerMachine
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s WorkerMachine -a SSISScaleOutWorker140
```

#### <a name="4-update-the-scale-out-worker-service-configuration-file"></a>4.更新 Scale Out Worker 服务配置文件
在辅助节点上更新 Scale Out Worker 服务配置文件 `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config`。 将 **WorkerHttpsCertThumbprint** 更新为新证书的指纹。

#### <a name="5-install-the-client-certificate-to-the-root-store-of-the-local-computer-on-the-master-node"></a>5.将客户端证书安装到主节点上本地计算机的根存储

#### <a name="6-restart-the-scale-out-worker-service"></a>6.重启 Scale Out Worker 服务

## <a name="next-steps"></a>后续步骤
有关详细信息，请参阅下文：
-   [Integration Services (SSIS) Scale Out Master](integration-services-ssis-scale-out-master.md)
-   [Integration Services (SSIS) Scale Out Worker](integration-services-ssis-scale-out-worker.md)