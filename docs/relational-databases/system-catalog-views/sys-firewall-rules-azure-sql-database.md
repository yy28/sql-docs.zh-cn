---
title: sys.firewall_rules （Azure SQL 数据库） |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.firewall_rules
- firewall_rules
- sys.firewall_rules_TSQL
- firewall_rules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- firewall_rules
- sys.firewall_rules
ms.assetid: 140d2cd8-9aa1-4cc5-870d-e1dbc873b3fe
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 090ec967e25fff1fac3761298214e0366c0f2478
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "33180253"
---
# <a name="sysfirewallrules-azure-sql-database"></a>sys.firewall_rules (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  返回有关与关联的服务器级防火墙设置的信息你[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 `sys.firewall_rules` 视图包含以下各列：  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|id|**INT**|服务器级防火墙设置的标识符。|  
|NAME|**NVARCHAR （128)**|您选择用来描述和区分服务器级防火墙设置的名称。|  
|start_ip_address|**VARCHAR(50)**|服务器级防火墙设置范围内的最低 IP 地址。 等于或大于此值的 IP 地址可能尝试连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器。 可能的最低 IP 地址为 `0.0.0.0`。|  
|end_ip_address|**VARCHAR(50)**|服务器级防火墙设置范围内的最高 IP 地址。 等于或小于此值的 IP 地址可能尝试连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器。 可能的最高 IP 地址为 `255.255.255.255`。<br /><br /> 注意： Windows Azure 连接尝试时才允许此这两个字段和**start_ip_address**字段等于`0.0.0.0`。|  
|create_date|**日期时间**|创建服务器级防火墙设置时的 UTC 日期和时间。<br /><br /> 注意： UTC 是协调世界时的首字母缩写。|  
|modify_date|**日期时间**|上次修改服务器级防火墙设置时的 UTC 日期和时间。|  
  
## <a name="remarks"></a>Remarks  
 若要删除数据库防火墙规则，请使用[sp_delete_firewall_rule &#40;Azure SQL 数据库&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)。 若要设置单个数据库的防火墙规则，请参阅[sys.database_firewall_rules &#40;Azure SQL 数据库&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)。 若要返回有关现有防火墙规则的信息，请查询 sys.firewall_rules （Azure SQL 数据库）。  
  
## <a name="permissions"></a>权限  
 对此视图的只读访问可供所有用户有权连接到**master**数据库。  
  
## <a name="see-also"></a>请参阅  
 [sys.database_firewall_rules &#40;Azure SQL 数据库&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)   
 [sp_set_firewall_rule &#40;Azure SQL 数据库&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [为数据库引擎访问配置 Windows 防火墙](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [Configure a Firewall for FILESTREAM 访问](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)   
 [将防火墙配置为允许报表服务器访问](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)   
 [如何：配置防火墙设置（Azure SQL 数据库）](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)  
  
  
