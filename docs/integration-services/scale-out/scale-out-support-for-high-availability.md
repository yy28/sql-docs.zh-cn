---
title: "SQL Server Integration Services (SSIS) 横向扩展对高可用性支持 |Microsoft 文档"
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
ms.openlocfilehash: 2405235bcfa09d2cc49e007f4eae6975d9ebf7a5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="scale-out-support-for-high-availability"></a>向外扩展以实现高可用性的支持

在 SSIS 向外扩展，通过正在执行的与多个缩放出工作人员的包提供辅助端高可用性。
使用实现主机端高可用性[Always On 的 SSIS 目录](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb)和 Windows 故障转移群集。 Windows 故障转移群集中托管的横向扩展 Master 多个实例。 当已关闭主节点上的缩放出主服务或 SSISDB 时，服务或辅助节点上的 SSISDB 将继续接受用户请求并与横向扩展辅助进程通信。 

若要设置的主机端高可用性，请按照下面的步骤。

## <a name="1-prerequisites"></a>1.必要條件
设置 Windows 故障转移群集。 请参阅 [安装适用于 Windows Server 2012 的故障转移群集功能和工具](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) 的博客文章以获取相关说明。 应在所有群集节点上安装功能和工具。

## <a name="2-install-scale-out-master-on-primary-node"></a>2.在主节点上安装缩放出 Master
数据库引擎服务、 Integration Services 和缩放出主机上安装的主节点缩放出母版。 

安装过程中，你应该 
### <a name="21-set-the-account-running-scale-out-master-service-to-a-domain-account"></a>2.1 设置为域帐户运行缩放出主服务的帐户。
此帐户应是可以在将来访问 Windows 故障转移群集中的辅助节点上的 SSISDB。 因为横向出主机服务和 SSISDB 可以故障转移单独，它们可能不是同一节点上。

![高可用性服务器配置](media/ha-server-config.PNG)

### <a name="22-include-scale-out-master-service-dns-host-name-in-the-cns-of-scale-out-master-certificate"></a>2.2 出母版包括缩放服务 DNS 主机名中的 Cn 的缩放出主证书。

将缩放出主终结点中使用此主机名。 

![HA 主配置](media/ha-master-config.PNG)

## <a name="3-install-scale-out-master-on-secondary-node"></a>3.在辅助节点上安装缩放出 Master
安装数据库引擎服务、 Integration Services 和缩放出主机在辅助节点上缩放出母版上。 

你应与主节点使用相同的缩放出主证书。 导出具有私钥主节点上的缩放出 Master SSL 证书并将其安装到辅助节点上的 loacl 机的根证书存储。 安装横向扩展 Master 时，请选择此证书。

![HA 主配置 2](media/ha-master-config2.PNG)

> [!Note]
> 可以通过重复辅助出主机缩放的操作，来设置多个备份缩放出母版。

## <a name="4-set-up-ssisdb-always-on"></a>4.在上始终设置 SSISDB

设置说明始终在 SSISDB 可以查看在[Always On 的 SSIS 目录 (SSISDB)](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb)。

此外，你需要创建 SSISDB 添加到可用性组的可用性 gourp 侦听器。 请参阅[创建或配置可用性组侦听器](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)。

## <a name="5-update-scale-out-master-service-configuration-file"></a>5.更新规模出 Master 服务配置文件
更新规模出 Master 服务配置文件，\<驱动程序\>: files\microsoft SQL Server\140\DTS\Binn\MasterSettings.config 主要和辅助节点上的。 更新**SqlServerName**到*[可用性组侦听器 DNS 名称]，[端口]*。

## <a name="6-enable-package-execution-logging"></a>6.启用包执行日志记录

SSISDB 中的日志记录可通过该登录名**# # MS_SSISLogDBWorkerAgentLogin # #**，其密码是自动生成。 若要使日志记录适用于所有副本的 SSISDB，执行以下操作。

### <a name="61-change-the-password-of-msssislogdbworkeragentlogin-on-primary-sql-server"></a>6.1 更改的密码**# # MS_SSISLogDBWorkerAgentLogin # #**主 Sql 服务器上。
### <a name="62-add-the-login-to-secondary-sql-server"></a>6.2 将登录名添加到辅助 Sql Server。
### <a name="63-update-connection-string-of-logging"></a>6.3 更新日志记录的连接的字符串。
调用存储的过程 [目录]。[update_logdb_info] 与 

@server_name=*[可用性组侦听器 DNS 名称]，[端口]* 

和@connection_string= 数据源 =*[可用性组侦听器 DNS 名称]*，*[端口]*; Initial Catalog = SSISDB;用户 Id = # # MS_SSISLogDBWorkerAgentLogin # #;密码 =*[Password]*];。

## <a name="7-congifure-scale-out-master-service-role-of-windows-failover-cluster"></a>7.Windows 故障转移群集的 Congifure 缩放出主机服务角色

在故障转移群集管理器，连接到群集的横向扩展。 选择群集，然后单击**操作**菜单中，然后**配置角色...**.

在弹出向上**高可用性向导**，选择**通用服务**中**选择角色**页面并选择 SQL Server 的集成服务缩放出 Master 14.0 中**选择服务**页。

在**客户端访问点**页上，输入的小数位数出 Master 服务 DNS 主机名。

![HA 向导 1](media/ha-wizard1.PNG)

完成该向导。

## <a name="8-update-master-address-in-ssisdb"></a>8.更新 Master SSISDB 中的地址

在主 SQL 服务器上，执行存储的过程 [SSIS]。[目录]。[update_master_address] 参数与@MasterAddress= N'https: / / [缩放出主机服务 DNS 主机名]: [Master 端口]。 

## <a name="9-add-scale-out-worker"></a>9.添加横向扩展辅助进程

现在，你可以添加横向扩展辅助进程的帮助[缩放出 Manager](integration-services-ssis-scale-out-manager.md)。 输入*[SQL Server 可用性组侦听器 DNS 名称]*，*[端口]*连接页中。





