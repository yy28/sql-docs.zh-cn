---
title: sys.firewall_rules （Azure SQL 数据库） |Microsoft Docs
ms.date: 03/26/2019
ms.prod: sql
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 2be0d498da026f386c3a89002cca621b19a2a15d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133986"
---
# <a name="sysfirewallrules-azure-sql-database"></a>sys.firewall_rules (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  返回有关与关联的服务器级防火墙设置的信息你[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 `sys.firewall_rules` 视图包含以下各列：  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|id|**INT**|服务器级防火墙设置的标识符。|  
|name|**NVARCHAR(128)**|您选择用来描述和区分服务器级防火墙设置的名称。|  
|start_ip_address|**VARCHAR(45)**|服务器级防火墙设置范围内的最低 IP 地址。 等于或大于此值的 IP 地址可能尝试连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器。 可能的最低 IP 地址为 `0.0.0.0`。|  
|end_ip_address|**VARCHAR(45)**|服务器级防火墙设置范围内的最高 IP 地址。 等于或小于此值的 IP 地址可能尝试连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器。 可能的最高 IP 地址为 `255.255.255.255`。<br /><br /> 注意:Windows Azure 连接尝试时才允许此这两个字段和**start_ip_address**字段等于`0.0.0.0`。|  
|create_date|**日期时间**|创建服务器级防火墙设置时的 UTC 日期和时间。<br /><br /> 注意:UTC 为通用协调时间的首字母缩写。|  
|modify_date|**日期时间**|上次修改服务器级防火墙设置时的 UTC 日期和时间。|  
  
## <a name="remarks"></a>备注

 返回到 Microsoft Azure SQL 数据库，使用与关联的数据库级防火墙设置有关的信息[sys.database_firewall_rules &#40;Azure SQL 数据库&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)。  
  
## <a name="permissions"></a>权限

 对此视图的只读访问可供有权连接到的所有用户**主**数据库。  
  
## <a name="see-also"></a>请参阅

[sp_set_firewall_rule（Azure SQL 数据库）](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
[sp_delete_firewall_rule &#40;Azure SQL 数据库&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)   
[sp_set_database_firewall_rule（Azure SQL 数据库）](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)  
[sp_delete_database_firewall_rule &#40;Azure SQL 数据库&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)  
[sys.database_firewall_rules &#40;Azure SQL 数据库&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
[为数据库引擎访问配置 Windows 防火墙](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)     
[将防火墙配置为进行 FILESTREAM 访问](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)  
[将防火墙配置为允许报表服务器访问](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md) 
