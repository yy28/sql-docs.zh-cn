---
title: sp_set_database_firewall_rule
titleSuffix: Azure SQL Database
ms.date: 08/04/2017
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_set_database_firewall_rule
- sp_set_database_firewall_rule_TSQL
- sys.sp_set_database_firewall_rule
- sys.sp_set_database_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_database_firewall_rule
- firewall_rules, setting database rules
ms.assetid: 8f0506b6-a4ac-4e4d-91db-8077c40cb17a
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: 2a465e03c3b77b8d05437fa0cfaf3354434ce973
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843846"
---
# <a name="sp_set_database_firewall_rule-azure-sql-database"></a>sp_set_database_firewall_rule (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  创建或更新 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]的数据库级防火墙规则。 可以为**master**数据库以及 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]上的用户数据库配置数据库防火墙规则。 使用包含的数据库用户时，数据库防火墙规则特别有用。 有关详细信息，请参阅 [包含的数据库用户 - 使你的数据库可移植](../../relational-databases/security/contained-database-users-making-your-database-portable.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_set_database_firewall_rule [@name = ] [N]'name'  
, [@start_ip_address =] 'start_ip_address'  
, [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 **[@name** =] [N] "*name*"  
 用来描述和区分数据库级防火墙设置的名称。 *name*为**nvarchar （128）** ，无默认值。 Unicode 标识符 `N` 是 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]的可选的。 
  
 **[@start_ip_address** =]"*start_ip_address*"  
 数据库级防火墙设置范围内的最低 IP 地址。 等于或大于此值的 IP 地址可能尝试连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 实例。 可能的最低 IP 地址为 `0.0.0.0`。 *start_ip_address*为**varchar （50）** ，无默认值。  
  
 [ **@end_ip_address** =]"*end_ip_address*"  
 数据库级防火墙设置范围内的最高 IP 地址。 等于或小于此值的 IP 地址可能尝试连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 实例。 可能的最高 IP 地址为 `255.255.255.255`。 *end_ip_address*为**varchar （50）** ，无默认值。  
  
 下表演示 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中支持的参数和选项。  
  
> [!NOTE]  
>  如果此字段和*start_ip_address*字段都等于 `0.0.0.0`，则允许 Azure 连接尝试。  
  
## <a name="remarks"></a>注释  
 数据库的数据库级防火墙设置的名称必须是唯一的。 如果为存储过程提供的数据库级防火墙设置的名称在数据库级防火墙设置表中已经存在，则将更新开始和结束 IP 地址。 否则，将创建新的数据库级防火墙设置。  
  
 当你添加一个数据库级防火墙设置，其中开始和结束 IP 地址等于 `0.0.0.0`时，你可以从任何 Azure 资源访问 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器中的数据库。 为*name*参数提供一个值，以帮助你记住防火墙设置的用途。  
  
## <a name="permissions"></a>权限  
 需要针对数据库的 CONTROL 权限。  
  
## <a name="examples"></a>示例  
 以下代码将创建一个名为 `Allow Azure` 的数据库级防火墙设置，该设置允许从 Azure 访问数据库。  
  
```  
-- Enable Azure connections.  
EXECUTE sp_set_database_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 以下代码仅为 IP 地址 `Example DB Setting 1` 创建一个称为 `0.0.0.4` 的数据库级防火墙设置。 然后，再次调用 `sp_set_database firewall_rule` 存储过程，以将结束 IP 地址更新为在该防火墙设置中 `0.0.0.6`。 这将创建一个范围，该范围允许 `0.0.0.4`、`0.0.0.5`和 `0.0.0.6` 的 IP 地址访问数据库。
  
```  
-- Create database-level firewall setting for only IP 0.0.0.4  
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.4';  
  
-- Update database-level firewall setting to create a range of allowed IP addresses
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.6';  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [AZURE SQL Database 防火墙](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [如何：配置防火墙设置（AZURE SQL Database）](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;Azure SQL 数据库&#41; ](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_delete_database_firewall_rule &#40;Azure SQL 数据库&#41; ](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [database_firewall_rules &#40;Azure SQL 数据库&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
  
