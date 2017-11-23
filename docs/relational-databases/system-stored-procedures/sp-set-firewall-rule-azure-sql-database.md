---
title: "sp_set_firewall_rule （Azure SQL 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 07/28/2016
ms.prod: 
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: 
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_set_firewall_rule
- sp_set_firewall_rule_TSQL
- sys.sp_set_firewall_rule
- sys.sp_set_firewall_rule_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sp_set_firewall_rule
- firewall_rules, setting server rules
ms.assetid: a974a561-5382-4039-8499-3a56767bcefe
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 38ef5788aba91bfde21df091321a69dbacbeb8e9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spsetfirewallrule-azure-sql-database"></a>sp_set_firewall_rule (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  创建或更新您的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器的服务器级防火墙设置。 此存储的过程才可用的服务器级别主体登录名或分配的 Azure Active Directory 主体到 master 数据库中。  
  
  
## <a name="syntax"></a>语法  
  
```
sp_set_firewall_rule [@name =] 'name', 
    [@start_ip_address =] 'start_ip_address', 
    [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 下表演示了支持的参数和选项中[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
|Name|数据类型|Description|  
|----------|--------------|-----------------|  
|[@name =] 'name'|**NVARCHAR （128)**|用来描述和区分服务器级防火墙设置的名称。|  
|[@start_ip_address =] 'start_ip_address|**VARCHAR(50)**|服务器级防火墙设置范围内的最低 IP 地址。 等于或大于此值的 IP 地址可能尝试连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器。 可能的最低 IP 地址为 `0.0.0.0`。|  
|[@end_ip_address =] 'end_ip_address|**VARCHAR(50)**|服务器级防火墙设置范围内的最高 IP 地址。 等于或小于此值的 IP 地址可能尝试连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器。 可能的最高 IP 地址为 `255.255.255.255`。<br /><br /> 注意： Azure 的连接尝试时才允许此这两个字段和*start_ip_address*字段等于`0.0.0.0`。|  
  
## <a name="remarks"></a>注释  
 服务器级防火墙设置的名称必须是唯一的。 如果为存储过程提供的设置的名称在防火墙设置表中已经存在，则将更新开始和结束 IP 地址。 否则，将创建新的服务器级防火墙设置。  
  
 添加服务器级防火墙设置的起始和结束 IP 地址都等于`0.0.0.0`，启用对你[!INCLUDE[ssSDS](../../includes/sssds-md.md)]从 Azure 的服务器。 向提供值*名称*参数将帮助你记住服务器级防火墙设置是什么。  
  
 在[!INCLUDE[ssSDS](../../includes/sssds-md.md)]、 登录数据需要进行身份验证连接和服务器级防火墙规则暂时缓存在每个数据库。 定期刷新此缓存。 若要强制执行身份验证缓存的刷新，并确保数据库具有登录名表的最新版本，执行[DBCC FLUSHAUTHCACHE &#40;Transact SQL &#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 只有服务器级别主体登录名由设置过程创建或指定为管理员可以创建或修改服务器级防火墙规则的 Azure Active Directory 主体。 用户必须连接到 master 数据库才能执行 sp_set_firewall_rule。  
  
## <a name="examples"></a>示例  
 下面的代码创建的服务器级防火墙设置调用`Allow Azure`这样的从 Azure 的访问。 执行以下操作在虚拟 master 数据库中。  
  
```  
-- Enable Windows Azure connections.  
exec sp_set_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 以下代码仅为 IP 地址 `Example setting 1` 创建一个称为 `0.0.0.2` 的服务器级防火墙设置。 然后，`sp_set_firewall_rule`再次调用存储的过程以更新到结束 IP 地址`0.0.0.4`，因为防火墙设置。 这将创建这样的 IP 地址范围`0.0.0.2`， `0.0.0.3`，和`0.0.0.4`来访问服务器。  
  
```  
-- Create server-level firewall setting for only IP 0.0.0.2  
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.2';  
  
-- Update server-level firewall setting to create a range of allowed IP addresses
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.4';  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [Azure SQL 数据库防火墙](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [如何： 配置防火墙设置 (Azure SQL Database)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sys.firewall_rules &#40;Azure SQL Database &#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)
