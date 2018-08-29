---
title: sys.database_firewall_rules （Azure SQL 数据库） |Microsoft Docs
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
- sys.database_firewall_rules_TSQL
- database_firewall_rules_TSQL
- sys.database_firewall_rules
- database_firewall_rules
dev_langs:
- TSQL
helpviewer_keywords:
- database_firewall_rules
- sys.database_firewall_rules
ms.assetid: 2e821593-3b9f-43d6-a99b-1ceffe177faf
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 068f01bc17a9f907aafaac6d39370be2a0480f57
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43038128"
---
# <a name="sysdatabasefirewallrules-azure-sql-database"></a>sys.database_firewall_rules (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  返回有关与关联的数据库级防火墙设置的信息你[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 在使用包含的数据库用户时，数据库级防火墙设置特别有用。 有关详细信息，请参阅 [包含的数据库用户 - 使你的数据库可移植](../../relational-databases/security/contained-database-users-making-your-database-portable.md)。  
  
 `sys.database_firewall_rules` 视图包含以下各列：  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|id|**INTEGER**|数据库级防火墙设置的标识符。|  
|NAME|**NVARCHAR （128)**|您选择用来描述和区分数据库级防火墙设置的名称。|  
|start_ip_address|**VARCHAR(50)**|数据库级防火墙设置范围内的最低 IP 地址。 等于或大于此值的 IP 地址可能尝试连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 实例。 可能的最低 IP 地址为 `0.0.0.0`。|  
|end_ip_address|**VARCHAR(50)**|防火墙设置范围内的最高 IP 地址。 等于或小于此值的 IP 地址可能尝试连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 实例。 可能的最高 IP 地址为 `255.255.255.255`。<br /><br /> 注意： Windows Azure 连接尝试时才允许此这两个字段和**start_ip_address**字段等于`0.0.0.0`。|  
|create_date|**日期时间**|创建数据库级防火墙设置时的 UTC 日期和时间。|  
|modify_date|**日期时间**|上次修改数据库级防火墙设置时的 UTC 日期和时间。|  
  
## <a name="remarks"></a>Remarks  
 若要删除数据库防火墙规则，请使用[sp_delete_database_firewall_rule &#40;Azure SQL 数据库&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)。 若要设置的所有防火墙规则[!INCLUDE[ssSDS](../../includes/sssds-md.md)]，请参阅[sp_set_firewall_rule &#40;Azure SQL 数据库&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)。 若要返回有关现有数据库的信息的防火墙规则，请查询[sys.database_firewall_rules （Azure SQL 数据库）](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)。  
  
## <a name="permissions"></a>Permissions  
 此视图现已推出**主**数据库和每个用户数据库中。 为具有连接到数据库的权限的所有用户提供对此视图的只读访问权限。  
  
## <a name="see-also"></a>请参阅  
 [sp_set_firewall_rule &#40;Azure SQL 数据库&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sys.database_firewall_rules （Azure SQL 数据库）](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)   
 [sp_delete_database_firewall_rule &#40;Azure SQL 数据库&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [为数据库引擎访问配置 Windows 防火墙](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [为进行 FILESTREAM 访问配置防火墙](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)   
 [将防火墙配置为允许报表服务器访问](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
  
  
