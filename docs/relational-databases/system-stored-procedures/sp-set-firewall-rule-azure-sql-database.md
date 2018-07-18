---
title: sp_set_firewall_rule （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
ms.prod: ''
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: ''
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_set_firewall_rule
- sp_set_firewall_rule_TSQL
- sys.sp_set_firewall_rule
- sys.sp_set_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_firewall_rule
- firewall_rules, setting server rules
ms.assetid: a974a561-5382-4039-8499-3a56767bcefe
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: e9315c7ca138d352ee9f0cdffca9abe3a2242dc0
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38056105"
---
# <a name="spsetfirewallrule-azure-sql-database"></a>sp_set_firewall_rule (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  创建或更新您的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器的服务器级防火墙设置。 此存储的过程才可用的服务器级别主体登录名或已分配的 Azure Active Directory 主体在 master 数据库中。  
  
  
## <a name="syntax"></a>语法  
  
```
sp_set_firewall_rule [@name =] 'name', 
    [@start_ip_address =] 'start_ip_address', 
    [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 下表演示了支持的参数和选项在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
|“属性”|数据类型|Description|  
|----------|--------------|-----------------|  
|[@name =] name|**NVARCHAR （128)**|用来描述和区分服务器级防火墙设置的名称。|  
|[@start_ip_address =] 'start_ip_address|**VARCHAR(50)**|服务器级防火墙设置范围内的最低 IP 地址。 等于或大于此值的 IP 地址可能尝试连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器。 可能的最低 IP 地址为 `0.0.0.0`。|  
|[@end_ip_address =] 'end_ip_address|**VARCHAR(50)**|服务器级防火墙设置范围内的最高 IP 地址。 等于或小于此值的 IP 地址可能尝试连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器。 可能的最高 IP 地址为 `255.255.255.255`。<br /><br /> 注意： Azure 连接尝试时才允许此这两个字段和*start_ip_address*字段等于`0.0.0.0`。|  
  
## <a name="remarks"></a>Remarks  
 服务器级防火墙设置的名称必须是唯一的。 如果为存储过程提供的设置的名称在防火墙设置表中已经存在，则将更新开始和结束 IP 地址。 否则，将创建新的服务器级防火墙设置。  
  
 添加服务器级防火墙设置的开始和结束 IP 地址都等于`0.0.0.0`，可以访问你[!INCLUDE[ssSDS](../../includes/sssds-md.md)]从 Azure 的服务器。 提供到值*名称*参数，它将帮助您记住服务器级防火墙设置的目的。  
  
 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中，对连接和服务器级别的防火墙规则进行身份验证时所需的登录数据会暂时缓存在每个数据库中。 此缓存定期刷新。 若要强制刷新身份验证缓存并确保数据库具有最新版本的登录名表，请执行 [DBCC FLUSHAUTHCACHE (Transact-SQL)](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)。  
  
## <a name="permissions"></a>权限  
 只有服务器级别主体登录名由预配过程创建或分配管理员可以创建或修改服务器级防火墙规则的 Azure Active Directory 主体。 用户必须连接到 master 数据库才能执行 sp_set_firewall_rule。  
  
## <a name="examples"></a>示例  
 下面的代码创建的服务器级防火墙设置调用`Allow Azure`，可以从 Azure 的访问。 在虚拟 master 数据库中执行以下操作。  
  
```  
-- Enable Windows Azure connections.  
exec sp_set_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 以下代码仅为 IP 地址 `Example setting 1` 创建一个称为 `0.0.0.2` 的服务器级防火墙设置。 然后，将`sp_set_firewall_rule`再次调用存储的过程来更新结束 IP 地址到`0.0.0.4`，因为防火墙设置。 这将创建允许的 IP 地址范围`0.0.0.2`， `0.0.0.3`，和`0.0.0.4`访问服务器。  
  
```  
-- Create server-level firewall setting for only IP 0.0.0.2  
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.2';  
  
-- Update server-level firewall setting to create a range of allowed IP addresses
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.4';  
  
```  
  
## <a name="see-also"></a>请参阅  
 [Azure SQL Database 防火墙](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [如何： 配置防火墙设置 （Azure SQL 数据库）](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sys.firewall_rules &#40;Azure SQL 数据库&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)
