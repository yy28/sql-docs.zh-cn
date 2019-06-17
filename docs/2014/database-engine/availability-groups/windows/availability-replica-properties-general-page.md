---
title: 可用性副本属性（“常规”页）| Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilityreplicaproperties.general.f1
ms.assetid: 8318fefb-e045-4fab-8507-e1951fc7cec6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 07652cec7b3b7a17c4b994eb68afd939e15244a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62791901"
---
# <a name="availability-replica-properties-general-page"></a>可用性副本属性（“常规”页）
  使用此对话框可以查看可用性副本的属性。  
  
## <a name="task-list"></a>任务列表  
 **查看可用性副本属性**  
  
-   [查看可用性副本属性 (SQL Server)](view-availability-replica-properties-sql-server.md)  
  
-   [使用 AlwaysOn 面板 (SQL Server Management Studio)](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="uielement-list"></a>UIElement 列表  
 **可用性组名称**  
 可用性组的名称。 这是在 Windows Server 故障转移群集 (WSFC) 内必须唯一的用户指定的名称。  
  
 **服务器实例**  
 承载此副本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的服务器名称；对于非默认实例，则为其实例名称。  
  
 **角色**  
 **主**  
 当前主副本。  
  
 **辅助副本**  
 当前辅助副本。  
  
 **正在解析**  
 当前该副本角色处于正在解析为主角色或辅助角色的进程中。  
  
 **可用性模式**  
 副本的可用性模式，可为下列值之一：  
  
 **异步提交**  
 主副本可以不必等待辅助副本将日志写入磁盘，即可提交事务。  
  
 **同步提交**  
 主副本等待提交给定的事务，直到辅助副本将事务写入磁盘。  
  
 有关详细信息，请参阅[可用性模式 （AlwaysOn 可用性组）](availability-modes-always-on-availability-groups.md)。  
  
 **Failover mode**  
 副本的故障转移模式，可为下列值之一：  
  
 **自动**  
 自动故障转移。 副本为自动故障转移的目标。 仅当可用性模式设置为同步提交时，才选择此选项。  
  
 **Manual**  
 手动故障转移。 副本仅能由数据库管理员手动进行故障转移。  
  
 **主角色中的连接**  
 当副本拥有主角色时支持的客户端连接类型。  
  
 **允许所有连接**  
 主副本中的数据库允许所有连接。 这是默认设置。  
  
 **允许读/写连接**  
 不允许 Application Intent 连接属性设置为 **ReadOnly** 的连接。 在 Application Intent 属性设置为 **ReadWrite** 或者未设置 Application Intent 连接属性时，将允许连接。  
  
 **可读取辅助角色**  
 正在履行辅助角色的可用性副本（也就是辅助副本）是否可以接受来自客户端的连接，可为下列值之一：  
  
 **是**  
 不允许与此副本的辅助数据库的直接连接。 它们不可用于读访问。 这是默认设置。  
  
 **仅限读意向**  
 仅允许与此副本的辅助数据库的直接只读连接。 辅助数据库全都可用于读访问。  
  
 **是**  
 允许与此副本的辅助数据库的所有连接，但仅限读访问。 辅助数据库全都可用于读访问。  
  
 有关详细信息，请参阅[活动次要副本：可读辅助副本 （AlwaysOn 可用性组）](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)。  
  
 **会话超时(秒)**  
 超时期限（秒）。 超时期限是指副本接收来自其他副本的消息而等待的最长时间，超过此时间，将主副本和辅助副本之间的连接视为已失败。 会话超时检测辅助副本是否与主副本相连接。 在检测到与辅助副本的连接失败时，主副本将辅助副本视为 NOT_SYNCHRONIZED。 在检测到与辅助副本的连接失败时，辅助副本只会尝试重新连接。  
  
> [!NOTE]  
>  会话超时不会导致自动故障转移。  
  
 **端点 URL**  
 用户指定的数据库镜像端点的字符串表示形式，该数据库镜像端点由用于数据同步的主副本和辅助副本之间的连接使用。 有关这些端点 URL 语法的信息，请参阅[在添加或修改可用性副本时指定端点 URL (SQL Server)](specify-endpoint-url-adding-or-modifying-availability-replica.md)。  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
