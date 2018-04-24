---
title: 更改故障转移群集实例的 IP 地址 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: failover-clusters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- modifying IP addresses
- failover clustering [SQL Server], IP addresses
- IP addresses [SQL Server]
- clusters [SQL Server], IP addresses
ms.assetid: b685f400-cbfe-4c5d-a070-227a1123dae4
caps.latest.revision: 33
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 692598e4fa27e18c40767d14e46aa48d4d03d265
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="change-the-ip-address-of-a-failover-cluster-instance"></a>更改故障转移群集实例的 IP 地址
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题说明如何使用故障转移群集管理器管理单元更改 AlwaysOn 故障转移群集实例 (FCI) 中的 IP 地址资源。 故障转移群集管理器管理单元是用于 Windows Server 故障转移群集 (WSFC) 服务的群集管理应用程序。  
  
-   **Before you begin:**  [Security](#Security)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
 在开始之前，请查看以下 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 联机丛书主题︰ [安装故障转移群集前的准备工作](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 若要维护或更新 FCI，您必须在 FCI 的所有节点上是拥有“作为服务登录”权限的本地管理员。  
  
##  <a name="WSFC"></a> 使用故障转移群集管理器管理单元  
 **更改 FCI 的 IP 地址资源**  
  
1.  打开故障转移群集管理器管理单元。  
  
2.  在左窗格中展开 **“服务和应用程序”** 节点，然后单击 FCI。  
  
3.  在右窗格的“服务器名称”类别下，右键单击该 SQL Server 实例，然后选择“属性”选项以打开“属性”对话框。  
  
4.  在 **“常规”** 选项卡上更改 IP 地址资源。  
  
5.  单击 **“确定”** 关闭对话框。  
  
6.  在右侧窗格中，右键单击“SQL IP Address1”（故障转移群集实例名称）并选择“脱机”。 将会看到 SQL IP Address1（故障转移群集实例名称）、SQL Network Name（故障转移群集实例名称）和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的状态从联机更改为脱机挂起，然后再更改为脱机。  
  
7.  在右侧窗格中，右键单击 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，然后选择“联机”。 将会看到 SQL IP Address1（故障转移群集实例名称）、SQL Network Name（故障转移群集实例名称）和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的状态从脱机更改为联机挂起，然后再更改为联机。  
  
8.  关闭故障转移群集管理器管理单元。  
  
  
