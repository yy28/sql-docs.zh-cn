---
title: 删除故障转移群集实例
description: 使用此过程可以卸载 SQL Server 故障转移群集实例。 本文包含继续操作操作前的重要注意事项。
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- clusters [SQL Server], removing failover clustered instance
- failover clustering [SQL Server], removing failover clustered instance
- uninstalling failover clustered instances
- removing failover clustered instances
ms.assetid: bf63353b-69cf-4c5c-98ea-7b151e36537f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: dba18abbd7eb5938b7f2fa4d0c3caff8d5d6f567
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85897671"
---
# <a name="remove-a-sql-server-failover-cluster-instance-setup"></a>删除 SQL Server 故障转移群集实例（安装程序）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  使用此过程可以卸载 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集实例。  
  
> [!IMPORTANT]  
>  若要更新或删除 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集，则您必须是本地管理员，且具有以服务登录到故障转移群集的所有节点的权限。  
  
 **开始之前**  
  
 请在卸载 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集之前考虑以下重要事项：  
  
-   如果意外卸载了 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 资源将无法启动。 若要重新安装 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client，请运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装程序来安装 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 必备组件。  
  
-   如果卸载具有多个 SQL IP 群集资源的故障转移群集，则必须使用群集管理器删除额外的 SQL IP 资源。  
  
 有关命令提示符语法的信息，请参阅 [从命令提示符安装 SQL Server 2016](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)。  
  
### <a name="to-uninstall-a-ssnoversion-failover-cluster"></a>卸载 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集  
  
1.  若要卸载 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集，请使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装程序提供的删除节点功能分别删除每个节点。 有关详细信息，请参阅[在 SQL Server 故障转移群集中添加或删除节点（安装程序）](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)。  
  
## <a name="see-also"></a>另请参阅  
 [查看和读取 SQL Server 安装程序日志文件](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
