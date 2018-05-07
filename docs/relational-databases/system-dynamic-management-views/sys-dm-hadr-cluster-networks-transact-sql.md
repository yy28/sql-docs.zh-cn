---
title: sys.dm_hadr_cluster_networks (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_hadr_cluster_networks
- sys.dm_hadr_cluster_networks_TSQL
- sys.dm_hadr_cluster_networks
- dm_hadr_cluster_networks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_cluster_networks dynamic management view
ms.assetid: ece32b15-d63f-4f93-92b7-e2930333e97a
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 003cb7c4a9bb64bc274830e42bfe717842de64f0
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmhadrclusternetworks-transact-sql"></a>sys.dm_hadr_cluster_networks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  为每个参与可用性组子网配置的 WSFC 群集成员都返回一行。 您可以使用此动态管理视图来验证为每个可用性副本配置的网络虚拟 IP。  
  
 主键： **member_name** + **network_subnet_IP** + **network_subnet_prefix_length**  
  
 > [!TIP]
 > 从[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，此动态管理视图支持 Alwayson 故障转移群集实例除了 Alwayson 可用性组。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar(128)**|WSFC 群集中某节点的计算机名称。|  
|**network_subnet_ip**|**nvarchar(48)**|该计算机所属子网的网络 IP 地址。 该地址可以是 IPv4 或 IPv6 地址。|  
|**network_subnet_ipv4_mask**|**nvarchar(45)**|指定 IP 地址所属子网的网络子网掩码。 **network_subnet_ipv4_mask**与 DHCP 子句中指定的 DHCP < network_subnet_option > 选项[CREATE AVAILABILITY GROUP](../../t-sql/statements/create-availability-group-transact-sql.md)或[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]语句。<br /><br /> NULL = IPv6 子网。|  
||||  
|**network_subnet_prefix_length**|**int**|指定该计算机所属子网的网络 IP 前缀长度。|  
|**is_public**|**bit**|该网络在 WSFC 群集中是专用还是公共网络，可为下列值之一：<br /><br /> 0 = 专用<br /><br /> 1 = 公共|  
|**is_ipv4**|**bit**|子网的类型，可为下列值之一：<br /><br /> 1 = IPv4<br /><br /> 0 = IPv6|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>另请参阅  
 [故障转移群集和 AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [监视可用性组 & #40;Transact SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys.dm_os_cluster_nodes &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [查询的 SQL Server 系统目录常见问题](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
