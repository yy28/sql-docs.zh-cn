---
title: sp_set_database_firewall_rule （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 08/04/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 6fa2b1effae12bd8132c331d4e1ba33055c656e0
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37984119"
---
# <a name="spsetdatabasefirewallrule-azure-sql-database"></a>sp_set_database_firewall_rule (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  创建或更新的数据库级防火墙规则在[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 可以为配置数据库防火墙规则**主**数据库，和上的用户数据库[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。 当使用包含的数据库用户时，数据库防火墙规则是特别有用。 有关详细信息，请参阅 [包含的数据库用户 - 使你的数据库可移植](../../relational-databases/security/contained-database-users-making-your-database-portable.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_set_database_firewall_rule [@name = ] [N]'name'  
, [@start_ip_address =] 'start_ip_address'  
, [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 **[@name**  =] [N]'*名称*  
 用来描述和区分数据库级防火墙设置的名称。 *名称*是**nvarchar （128)** ，无默认值。 Unicode 标识符`N`是可选的[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。 
  
 **[@start_ip_address**  =] '*start_ip_address*  
 数据库级防火墙设置范围内的最低 IP 地址。 等于或大于此值的 IP 地址可能尝试连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 实例。 可能的最低 IP 地址为 `0.0.0.0`。 *start_ip_address*是**varchar(50)** ，无默认值。  
  
 [**@end_ip_address** =] '*end_ip_address*  
 数据库级防火墙设置范围内的最高 IP 地址。 等于或小于此值的 IP 地址可能尝试连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 实例。 可能的最高 IP 地址为 `255.255.255.255`。 *end_ip_address*是**varchar(50)** ，无默认值。  
  
 下表演示了支持的参数和选项在[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
> [!NOTE]  
>  时，才允许 azure 连接尝试这两个此字段和*start_ip_address*字段等于`0.0.0.0`。  
  
## <a name="remarks"></a>Remarks  
 数据库的数据库级防火墙设置的名称必须是唯一的。 如果为存储过程提供的数据库级防火墙设置的名称在数据库级防火墙设置表中已经存在，则将更新开始和结束 IP 地址。 否则，将创建新的数据库级防火墙设置。  
  
 如果添加的开始和结束 IP 地址都等于数据库级防火墙设置`0.0.0.0`，启用访问权限中的数据库[!INCLUDE[ssSDS](../../includes/sssds-md.md)]从任何 Azure 资源的服务器。 提供到值*名称*参数，它将帮助您记住防火墙设置的目的。  
  
## <a name="permissions"></a>权限  
 需要针对数据库的 CONTROL 权限。  
  
## <a name="examples"></a>示例  
 下面的代码创建的数据库级防火墙设置调用`Allow Azure`启用到你的数据库从 Azure 访问。  
  
```  
-- Enable Azure connections.  
EXECUTE sp_set_database_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 以下代码仅为 IP 地址 `Example DB Setting 1` 创建一个称为 `0.0.0.4` 的数据库级防火墙设置。 然后，将`sp_set_database firewall_rule`再次调用存储的过程来更新结束 IP 地址到`0.0.0.6`，因为防火墙设置。 这将创建允许的 IP 地址范围`0.0.0.4`， `0.0.0.5`，和`0.0.0.6`来访问数据库。
  
```  
-- Create database-level firewall setting for only IP 0.0.0.4  
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.4';  
  
-- Update database-level firewall setting to create a range of allowed IP addresses
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.6';  
  
```  
  
## <a name="see-also"></a>请参阅  
 [Azure SQL Database 防火墙](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [如何： 配置防火墙设置 （Azure SQL 数据库）](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;Azure SQL 数据库&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_delete_database_firewall_rule &#40;Azure SQL 数据库&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [sys.database_firewall_rules &#40;Azure SQL 数据库&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
  
