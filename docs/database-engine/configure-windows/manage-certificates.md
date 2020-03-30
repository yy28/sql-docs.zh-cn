---
title: 证书管理（SQL Server 配置管理器）| Microsoft Docs
ms.custom: ''
ms.date: 01/16/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b98f52d7c8e23530c13da6ad44d90090998ac09e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68212749"
---
# <a name="certificate-management-sql-server-configuration-manager"></a>证书管理（SQL Server 配置管理器）

本主题介绍如何在 SQL Server Always On 故障转移群集或可用性组拓扑上部署和管理证书。

SSL/TLS 证书广泛用于保护对 SQL Server 的访问。 对于早期版本的 SQL Server，具有大型 SQL Server 资产的组织通常必须花费大量精力，通过开发脚本和运行手动命令，来维护其 SQL Server 证书基础结构。 借助 SQL Server 2019，证书管理已集成到 SQL Server 配置管理器，以简化诸如以下常见任务： 

* 查看和验证安装在 SQL Server 实例上的证书。 
* 确定可能即将到期的证书。 
* 从包含主要副本的节点在可用性组计算机之间部署证书。 
* 从活动节点在参与到故障转移群集实例的计算机之间部署证书。

> [!NOTE]
> 通过较低版本的 SQL Server（从 SQL Server 2008 开始），可使用 SQL Server 配置管理器中的证书管理功能。

##  <a name="to-install-a-certificate-for-a-single-sql-server-instance"></a><a name="provision-single-server-cert"></a> 为单一 SQL Server 实例安装证书  
  
1. 在 SQL Server 配置管理器的控制台窗格中，展开“SQL Server 网络配置”  。  
  
2. 右键单击“**实例名称** 的协议”，然后选择“属性” *&lt;&gt;*  。  
  
3. 选择“证书”选项卡，然后选择“导入”   。  
  
4. 选择“浏览”，然后选择证书文件  。  
  
5. 选择“下一步”，验证证书  。 如果没有错误，请选择“下一步”，将证书导入到本地实例  。  
  
 
##  <a name="to-install-a-certificate-in-a-failover-cluster-configuration"></a><a name="provision-failover-cluster-cert"></a> 在故障转移群集配置中安装证书  
  
1. 在 SQL Server 配置管理器的控制台窗格中，展开“SQL Server 网络配置”  。
  
2. 右键单击“**实例名称** 的协议”，然后选择“属性” *&lt;&gt;*  。 

3. 选择“证书”选项卡，然后选择“导入”   。

4. 选择证书类型，以及是仅导入当前节点还是导入每个单独的群集节点。

5. 如果为单一节点安装证书，请选择“浏览”并选择证书文件  。 然后跳到步骤 8。

6. 如果为每个节点安装证书，请选择“下一步”，列出可能的所有者节点  。 当前 SQL Server FCI 的可能的所有者是预先选择的。

7. 选择“下一步”，选择要导入的证书  。

8. 出现提示时，输入密码。 在验证后，查找任何警告或错误。

9. 选择“下一步”，导入所选证书  。

> [!NOTE]
> 在 SQL Server 故障转移群集实例的活动节点中完成这些步骤。 用户必须拥有所有群集节点的管理员权限。

##  <a name="to-install-a-certificate-in-an-availability-group-configuration"></a><a name="provision-availability-group-cert"></a> 在可用性组配置中安装证书  
  
1. 在 SQL Server 配置管理器的控制台窗格中，展开“SQL Server 网络配置”  。
  
2. 右键单击“**实例名称** 的协议”，然后选择“属性” *&lt;&gt;*  。  
  
3. 选择“证书”选项卡，然后选择“导入”   。  
  
4. 选择证书类型，然后选择“下一步”，从已知的可用性组列表中进行选择  。  

5. 选择“下一步”，选择每个副本节点的证书  。 证书应具有与节点的 NetBIOS 名一致的文件名。

6. 选择“下一步”，在每个节点上导入证书  。


> [!NOTE]
> 从包含可用性组主要副本的节点中完成这些步骤。 用户必须拥有所有群集节点的管理员权限。

