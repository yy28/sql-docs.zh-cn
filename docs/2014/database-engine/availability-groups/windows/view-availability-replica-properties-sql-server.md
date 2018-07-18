---
title: 查看可用性副本属性 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ', policies'
ms.assetid: 14fed3c4-8ecc-4e1c-931d-a7ec1e9f9e90
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c9c8ce45ca1ae4efdb65d8d1aae44261be80a0a5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37282194"
---
# <a name="view-availability-replica-properties-sql-server"></a>查看可用性副本属性 (SQL Server)
  本主题介绍如何通过使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 中的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]查看 AlwaysOn 可用性组的可用性副本属性。  
  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **查看和更改可用性副本的属性**  
  
1.  在对象资源管理器中，连接到承载主副本的服务器实例，然后展开服务器树。  
  
2.  依次展开 **“AlwaysOn 高可用性”** 节点和 **“可用性组”** 节点。  
  
3.  展开可用性副本所属的可用性组，然后展开 **“可用性副本”** 节点。  
  
4.  右键单击要查看其属性的可用性副本，然后选择“属性”命令。  
  
5.  在 **“可用性副本属性”** 对话框中，使用 **“常规”** 页查看该副本的属性。 如果连接到主副本，您可以更改下列属性：可用性模式、故障转移模式、主角色的连接访问权限、辅助角色（可读取的辅助副本）的读取访问权限以及会话超时值。 有关详细信息，请参阅[可用性副本属性&#40;常规页&#41;](availability-replica-properties-general-page.md)。  
  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **查看可用性副本的属性和状态**  
  
 若要查看可用性副本的属性和状态，请使用以下视图和系统函数：  
  
 [sys.availability_replicas](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql)  
 为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的本地实例承载其可用性副本的每个可用性组中的每个可用性副本返回一行。  
  
 **列名：** replica_id、group_id、replica_metadata_id、replica_server_name、owner_sid、endpoint_url、availability_mode、availability_mode_desc、failover_mode、failover_mode_desc、session_timeout、primary_role_allow_connections、primary_role_allow_connections_desc、secondary_role_allow_connections、secondary_role_allow_connections_desc、create_date、modify_date、backup_priority、read_only_routing_url  
  
 [sys.availability_read_only_routing_lists](/sql/relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql)  
 为 WSFC 故障转移群集中 AlwaysOn 可用性组的每个可用性副本的只读路由列表返回一行。  
  
 **列名：** replica_id、routing_priority、read_only_replica_id  
  
 [sys.dm_hadr_availability_replica_cluster_nodes](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-nodes-transact-sql)  
 为 Windows Server 故障转移群集 (WSFC) 群集中 AlwaysOn 可用性组的每个可用性副本（不论联接状态如何）都返回一行。  
  
 **列名：** group_name、replica_server_name、node_name  
  
 [sys.dm_hadr_availability_replica_cluster_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql)  
 为 Windows Server 故障转移群集 (WSFC) 群集中所有 AlwaysOn 可用性组（不论副本位于何处）的每个副本（不论联接状态如何）都返回一行。  
  
 **列名：** replica_id、replica_server_name、group_id、join_state、join_state_desc  
  
 [sys.dm_hadr_availability_replica_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql)  
 返回一行以显示每个本地可用性副本的状态，并为同一可用性组中的每个远程可用性副本返回一行。  
  
 **列名：** replica_id、group_id、is_local、role、role_desc、operational_state、operational_state_desc、connected_state、connected_state_desc、recovery_health、recovery_health_desc、synchronization_health、synchronization_health_desc、last_connect_error_number、last_connect_error_description 和 last_connect_error_timestamp  
  
 [sys.fn_hadr_backup_is_preferred_replica](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)  
 确定当前副本是否为首选备份副本。 如果当前服务器实例上的数据库是首选副本，则返回 1。 否则，返回 0。  
  
> [!NOTE]  
>  有关可用性副本的性能计数器（ **SQLServer:Availability Replica**  性能对象）的信息，请参阅 [SQL Server，可用性副本](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)。  
  
  
##  <a name="RelatedTasks"></a> 相关任务  
 **查看有关可用性组的信息**  
  
-   [查看可用性组属性 (SQL Server)](view-availability-group-properties-sql-server.md)  
  
-   [查看可用性组侦听程序属性 (SQL Server)](view-availability-group-listener-properties-sql-server.md)  
  
-   [针对 AlwaysOn 可用性组运行问题的 AlwaysOn 策略&#40;SQL Server&#41;](always-on-policies-for-operational-issues-always-on-availability.md)
  
-   [使用 AlwaysOn 面板 (SQL Server Management Studio)](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
-   [监视可用性组 (Transact-SQL)](monitor-availability-groups-transact-sql.md)  
  
 **管理可用性副本**  
  
-   [将辅助副本添加到可用性组 (SQL Server)](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [将辅助副本联接到可用性组 (SQL Server)](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [配置对可用性副本的只读访问 (SQL Server)](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [更改可用性副本的可用性模式 (SQL Server)](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [更改可用性副本的故障转移模式 (SQL Server)](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [更改可用性副本的会话超时期限 (SQL Server)](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
-   [将次要副本从可用性组删除 (SQL Server)](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
 **管理可用性数据库**  
  
-   [将数据库添加到可用性组 (SQL Server)](availability-group-add-a-database.md)  
  
-   [将辅助数据库联接到可用性组 (SQL Server)](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [挂起可用性数据库 (SQL Server)](suspend-an-availability-database-sql-server.md)  
  
-   [恢复可用性数据库 (SQL Server)](resume-an-availability-database-sql-server.md)  
  
-   [将辅助数据库从可用性组删除 (SQL Server)](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [将主数据库从可用性组删除 (SQL Server)](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [监视可用性组 (Transact-SQL)](monitor-availability-groups-transact-sql.md)   
 [针对 AlwaysOn 可用性组运行问题的 AlwaysOn 策略&#40;SQL Server&#41;](always-on-policies-for-operational-issues-always-on-availability.md)   
 [管理可用性组 (SQL Server)](administration-of-an-availability-group-sql-server.md)  
  
  
