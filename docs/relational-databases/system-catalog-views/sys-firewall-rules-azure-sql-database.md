---
title: sys. firewall_rules （Azure SQL Database） |Microsoft Docs
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
ms.openlocfilehash: 91c3a4101f19afe4a986514fea8dab207c6d9b48
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "70155544"
---
# <a name="sysfirewall_rules-azure-sql-database"></a>sys.firewall_rules (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  返回与[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]关联的服务器级防火墙设置的相关信息。  
  
 `sys.firewall_rules` 视图包含以下各列：  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|ID|**整形**|服务器级防火墙设置的标识符。|  
|name|**NVARCHAR （128）**|您选择用来描述和区分服务器级防火墙设置的名称。|  
|start_ip_address|**VARCHAR （45）**|服务器级防火墙设置范围内的最低 IP 地址。 等于或大于此值的 IP 地址可能尝试连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器。 可能的最低 IP 地址为 `0.0.0.0`。|  
|end_ip_address|**VARCHAR （45）**|服务器级防火墙设置范围内的最高 IP 地址。 等于或小于此值的 IP 地址可能尝试连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器。 可能的最高 IP 地址为 `255.255.255.255`。<br /><br /> 注意：如果此字段和**start_ip_address**字段都等于`0.0.0.0`，则允许 Azure 连接尝试。|  
|create_date|**型**|创建服务器级防火墙设置时的 UTC 日期和时间。<br /><br /> 注意： UTC 是协调世界时的首字母缩写词。|  
|modify_date|**型**|上次修改服务器级防火墙设置时的 UTC 日期和时间。|  
  
## <a name="remarks"></a>备注

 若要返回有关与您的 Microsoft Azure SQL 数据库关联的数据库级防火墙设置的信息，请使用[AZURE SQL 数据库&#41;&#40;database_firewall_rules ](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)。  
  
## <a name="permissions"></a>权限

 对此视图的只读访问权限可供有权连接到**master**数据库的所有用户使用。  
  
## <a name="see-also"></a>另请参阅

[sp_set_firewall_rule（Azure SQL 数据库）](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
[Azure SQL Database &#40;sp_delete_firewall_rule&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)   
[sp_set_database_firewall_rule（Azure SQL 数据库）](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)  
[Azure SQL Database &#40;sp_delete_database_firewall_rule&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)  
[database_firewall_rules &#40;Azure SQL 数据库&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
[为数据库引擎访问配置 Windows 防火墙](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)     
[将防火墙配置为进行 FILESTREAM 访问](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)  
[将防火墙配置为允许报表服务器访问](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md) 
