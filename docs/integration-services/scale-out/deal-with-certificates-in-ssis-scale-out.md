---
title: "处理在 Sql Server 的集成服务向外扩展的证书 |Microsoft 文档"
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2970b2b2cc7cf30c18a203ebbb92b5418bfc9be5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="deal-with-certificates-in-sql-server-integration-services-scale-out"></a>处理在 SQL Server 的集成服务向外扩展的证书

若要保护出母版横向和横向扩展辅助进程之间的通信，两个证书中使用横向扩展，即缩放出主证书和横向扩展辅助证书。 

## <a name="scale-out-master-certificate"></a>缩放出 Master 证书

在大多数情况下，缩放出 Master 安装期间配置缩放出主证书。

在**Integration Services 横向扩展配置的主节点**页上的 SQL Server 安装向导中，你可以选择创建新的自签名的 SSL 证书或使用现有的 SSL 证书。

![主机配置](media/master-config.PNG)

如果你没有特殊要求的证书，你可以选择创建新的自签名的 SSL 证书。 证书中，可以进一步指定 Cn。 请确保 Cn 中包含更高版本使用横向扩展辅助进程的主终结点的主机名。 默认情况下，将包含计算机名称和主节点的 ip。 

如果你选择使用现有证书，单击"浏览..."选择 SSL 证书从**根**本地计算机证书存储。

### <a name="change-scale-out-master-certificate"></a>更改缩放出 Master 证书

你可能想要更改由于证书过期或其他原因你缩放出主证书。 请执行下列步骤：

#### <a name="1-create-a-ssl-certificate"></a>1.创建 SSL 证书。
创建并在主机上安装 SSL 证书使用以下命令的节点：
```dos
MakeCert.exe -n CN={master endpoint host} SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```
例如：
```dos
MakeCert.exe -n CN=MasterMachine SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```

#### <a name="2-bind-the-certificate-to-master-port"></a>2.将证书绑定到主端口
请检查该命令的原始绑定：
```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```
例如：
```dos
netsh http show sslcert ipport=0.0.0.0:8391
```
删除原始的绑定并设置新的绑定，使用以下命令：
```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={SSL Certificate Thumbprint} certstorename=Root appid={original appid}
```
例如：
```dos
netsh http delete sslcert ipport=0.0.0.0:8391
netsh http add sslcert ipport=0.0.0.0:8391 certhash=01d207b300ca662f479beb884efe6ce328f77d53 certstorename=Root appid={a1f96506-93e0-4c91-9171-05a2f6739e13}
```
#### <a name="3-update-scale-out-master-service-configuration-file"></a>3.更新规模出 Master 服务配置文件
更新规模出 Master 服务配置文件，\<驱动程序\>: files\microsoft SQL Server\140\DTS\Binn\MasterSettings.config，在主服务器节点。 更新**SSLCertThumbprint**到新的 SSL 证书的指纹。

#### <a name="4-restart-scale-out-master-service"></a>4.重新启动缩放出主机服务

#### <a name="5-reconnect-scale-out-worker-to-scale-out-master"></a>5.重新连接横向扩展辅助横向扩展 Master
对于每个缩放出工作进程，可以删除工作线程，将其与重新添加[缩放出 Manager](integration-services-ssis-scale-out-manager.md)或者执行 5.1 到 5.3 下面的步骤：

5.1 客户端将 SSL 证书安装到辅助节点上的本地计算机的根存储区

5.2 出辅助服务配置文件更新横向扩展辅助服务配置文件中，更新规模\<驱动程序\>: files\microsoft SQL Server\140\DTS\Binn\WorkerSettings.config 辅助节点上的。 更新**MasterHttpsCertThumbprint**到新的 SSL 证书的指纹。

5.3 重新缩放启动出 Worker 服务


## <a name="scale-out-worker-certificate"></a>横向扩展辅助证书

在横向扩展辅助进程的安装过程中自动生成横向扩展辅助证书。 

### <a name="change-scale-out-worker-certificate"></a>更改缩放出辅助证书

在你想要更改缩放出工作线程证书的情况下，请按照下面的步骤。

#### <a name="1-create-a-certificate"></a>1.创建证书
创建并使用以下命令安装证书：
```dos
MakeCert.exe -n CN={worker machine name};CN={worker machine ip} SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
例如：
```dos
MakeCert.exe -n CN=WorkerMachine;CN=10.0.2.8 SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
#### <a name="2-install-the-client-certificate-to-the-root-store-of-local-machine-on-worker-node"></a>2.将客户端证书安装到辅助节点上的本地计算机的根存储

#### <a name="3-give-service-access-to-the-certificate"></a>3.为证书提供服务的访问权限
删除旧证书并授予横向扩展辅助服务访问的命令的新证书：
```dos
certmgr.exe /del /c /s /r localmachine My /n {CN of the old certificate}
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the new certificate} -a {the account running Scale Out Worker service}
```
例如：
```dos
certmgr.exe /del /c /s /r localmachine My /n WorkerMachine
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s WorkerMachine -a SSISScaleOutWorker140
```
#### <a name="4-update-scale-out-worker-configuration-file"></a>4.更新横向扩展辅助角色配置文件
更新横向扩展辅助服务配置文件，\<驱动程序\>: files\microsoft SQL Server\140\DTS\Binn\WorkerSettings.config 辅助节点上的。 更新**WorkerHttpsCertThumbprint**到新的证书的指纹。

#### <a name="5-install-the-client-certificate-to-the-root-store-of-local-machine-on-master-node"></a>5.客户端证书安装到的根存储中在主机上的本地计算机节点

#### <a name="6-restart-scale-out-worker-service"></a>6.重新启动横向扩展辅助服务

