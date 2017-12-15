---
title: "SQL Server Integration Services (SSIS) Scale Out 对高可用性的支持 | Microsoft Docs"
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
ms.openlocfilehash: 2202b61a9efce26edb0edcef53204351338ecee6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="scale-out-support-for-high-availability"></a>Scale Out 对高可用性的支持

在 SSIS Scale Out 中，通过使用多个 Scale Out Worker 来执行包，可提供辅助节点端的高可用性。
主节点端的高可用性则通过[针对 SSIS 目录的 Always On](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) 和 Windows 故障转移群集实现。 Scale Out Master 的多个实例托管在 Windows 故障转移群集中。 当主节点上的 Scale Out Master 服务或 SSISDB 关闭时，辅助节点上的该服务或 SSISDB 将继续接受用户请求并与 Scale Out Worker 通信。 

若要设置主节点端的高可用性，请按照以下步骤操作。

## <a name="1-prerequisites"></a>1.先决条件
设置 Windows 故障转移群集。 请参阅 [安装适用于 Windows Server 2012 的故障转移群集功能和工具](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) 的博客文章以获取相关说明。 应在所有群集节点上安装功能和工具。

## <a name="2-install-scale-out-master-on-primary-node"></a>2.在主节点上安装 Scale Out Master
在用于 Scale Out Master 的主节点上安装数据库引擎服务、Integration Services 和 Scale Out Master。 

在安装过程中，应当 
### <a name="21-set-the-account-running-scale-out-master-service-to-a-domain-account"></a>2.1 将运行 Scale Out Master 服务的帐户设置为域帐户。
此帐户将来应当能访问 Windows 故障转移群集中辅助节点上的 SSISDB。 由于 Scale Out Master 服务和 SSISDB 可以分开进行故障转移，因此，它们可能位于不同的节点上。

![HA 服务器配置](media/ha-server-config.PNG)

### <a name="22-include-scale-out-master-service-dns-host-name-in-the-cns-of-scale-out-master-certificate"></a>2.2 在 Scale Out Master 证书的 CN 中包含 Scale Out Master 服务 DNS 主机名。

此主机名将用于 Scale Out Master 终结点。 

![HA 主节点配置](media/ha-master-config.PNG)

## <a name="3-install-scale-out-master-on-secondary-node"></a>3.在辅助节点上安装 Scale Out Master
在用于 Scale Out Master 的辅助节点上安装数据库引擎服务、Integration Services 和 Scale Out Master。 

应使用与主节点相同的 Scale Out Master 证书。 使用私钥导出主节点上的 Scale Out Master SSL 证书，将其安装到辅助节点上本地计算机的根证书存储中。 安装 Scale Out Master 时，请选择此证书。

![HA 主节点配置 2](media/ha-master-config2.PNG)

> [!Note]
> 通过对辅助 Scale Out Master 重复这些操作，可设置多个备份 Scale Out Master。

## <a name="4-set-up-ssisdb-always-on"></a>4.设置 SSISDB Always On

[针对 SSIS 目录 (SSISDB) 的 Always On](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) 提供了有关为 SSISDB 设置 Always On 的说明。

此外，还需为 SSISDB 添加到的可用性组创建可用性组侦听程序。 请参阅[创建或配置可用性组侦听程序](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)。

## <a name="5-update-scale-out-master-service-configuration-file"></a>5.更新 Scale Out Master 服务配置文件
更新主节点和辅助节点上的 Scale Out Master 服务配置文件 \<驱动程序\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config。 将 **SqlServerName** 更新为 *[可用性组侦听程序 DNS 名称],[端口]*。

## <a name="6-enable-package-execution-logging"></a>6.启用包执行日志记录

使用登录名 **##MS_SSISLogDBWorkerAgentLogin##**（其密码是自动生成的）在 SSISDB 中进行日志记录。 若要让日志记录适用于 SSISDB 的所有副本，请执行以下操作。

### <a name="61-change-the-password-of-msssislogdbworkeragentlogin-on-primary-sql-server"></a>6.1 更改主 SQL Server 上 **##MS_SSISLogDBWorkerAgentLogin##** 的密码。
### <a name="62-add-the-login-to-secondary-sql-server"></a>6.2 将该登录名添加到辅助 SQL Server。
### <a name="63-update-connection-string-of-logging"></a>6.3 更新日志记录的连接字符串。
调用 

@server_name 为 '*[可用性组侦听程序 DNS 名称],[端口]*' 

且 @connection_string 为 'Data Source=*[可用性组侦听程序 DNS 名称]*,*[端口]*;Initial Catalog=SSISDB;User Id=##MS_SSISLogDBWorkerAgentLogin##;Password=*[密码]*];' 的存储过程 [catalog].[update_logdb_info]。

## <a name="7-congifure-scale-out-master-service-role-of-windows-failover-cluster"></a>7.配置 Windows 故障转移群集的 Scale Out Master 服务角色

在故障转移群集管理器中，连接到 Scale Out 的群集。选择该群集，单击菜单中的“操作”，然后单击“配置角色...”。

在弹出的“高可用性向导”中，选择“选择角色”页中的“通用服务”，然后选择“选择服务”页中的 SQL Server Integration Services Scale Out Master 14.0。

在“客户端访问点”页中，输入 Scale Out Master 服务 DNS 主机名。

![HA 向导 1](media/ha-wizard1.PNG)

完成该向导。

## <a name="8-update-master-address-in-ssisdb"></a>8.更新 SSISDB 中的主节点地址

在主 SQL Server 上，执行参数 @MasterAddress 为 N'https://[Scale Out Master 服务 DNS 主机名]:[主端口]' 的存储过程 [SSIS].[catalog].[update_master_address]。 

## <a name="9-add-scale-out-worker"></a>9.添加 Scale Out Worker

现在，可以借助 [Scale Out Manager](integration-services-ssis-scale-out-manager.md) 添加 Scale Out Worker。 在连接页中输入 *[SQL Server 可用性组侦听程序 DNS 名称]*,*[端口]*。




