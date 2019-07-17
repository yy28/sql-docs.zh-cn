---
title: sp_helpdistributor (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdistributor_TSQL
- sp_helpdistributor
helpviewer_keywords:
- sp_helpdistributor
ms.assetid: 37b0983e-3b69-4f0f-977e-20efce0a0b97
author: stevestein
ms.author: sstein
ms.openlocfilehash: 42c350876037c83505860c65b26f4302d75b6eed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122559"
---
# <a name="sphelpdistributor-transact-sql"></a>sp_helpdistributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出有关分发服务器、 分发数据库、 工作目录的信息和[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理用户的帐户。 该存储过程在发布服务器上对发布数据库或任何数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpdistributor [ [ @distributor= ] 'distributor' OUTPUT ]  
    [ , [ @distribdb= ] 'distribdb' OUTPUT ]  
    [ , [ @directory= ] 'directory' OUTPUT ]  
    [ , [ @account= ] 'account' OUTPUT ]  
    [ , [ @min_distretention= ] min_distretention OUTPUT ]  
    [ , [ @max_distretention= ] max_distretention OUTPUT ]  
    [ , [ @history_retention= ] history_retention OUTPUT ]  
    [ , [ @history_cleanupagent= ] 'history_cleanupagent' OUTPUT ]  
    [ , [ @distrib_cleanupagent = ] 'distrib_cleanupagent' OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @local = ] 'local' ]  
    [ , [ @rpcsrvname= ] 'rpcsrvname' OUTPUT ]  
    [ , [ @publisher_type = ] 'publisher_type' OUTPUT ]  
```  
  
## <a name="arguments"></a>参数  
`[ @distributor = ] 'distributor' OUTPUT` 是分发服务器的名称。 分发服务器是**sysname**，默认值为 **%** ，这是唯一返回结果集的值。  
  
`[ @distribdb = ] 'distribdb' OUTPUT` 是分发数据库的名称。 *distribdb*是**sysname**，默认值为 **%** ，这是唯一返回结果集的值。  
  
`[ @directory = ] 'directory' OUTPUT` 是工作目录。 *目录*是**nvarchar(255)** ，默认值为 **%** ，这是唯一返回结果集的值。  
  
`[ @account = ] 'account' OUTPUT` 是[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 用户帐户。 *帐户*是**nvarchar(255)** ，默认值为 **%** ，这是唯一返回结果集的值。  
  
`[ @min_distretention = ] _min_distretentionOUTPUT` 是最小分发保持期，以小时为单位。 *min_distretention*是**int**，默认值为 **-1**。  
  
`[ @max_distretention = ] _max_distretentionOUTPUT` 是最大分发保持期，以小时为单位。 *max_distretention*是**int**，默认值为 **-1**。  
  
`[ @history_retention = ] _history_retentionOUTPUT` 是的历史记录保持期，以小时为单位。 *history_retention*是**int**，默认值为 **-1**。  
  
`[ @history_cleanupagent = ] 'history_cleanupagent' OUTPUT` 是历史记录清除代理的名称。 *history_cleanupagent*是**nvarchar(100)** ，默认值为 **%** ，这是唯一返回结果集的值。  
  
`[ @distrib_cleanupagent = ] 'distrib_cleanupagent' OUTPUT` 是分发清除代理的名称。 *distrib_cleanupagent*是**nvarchar(100)** ，默认值为 **%** ，这是唯一返回结果集的值。  
  
`[ @publisher = ] 'publisher'` 是发布服务器的名称。 *发布服务器*是**sysname**，默认值为 NULL。  
  
`[ @local = ] 'local'` 是是否[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]应获得本地服务器值。 *本地*是**nvarchar(5)** ，默认值为 NULL。  
  
`[ @rpcsrvname = ] 'rpcsrvname' OUTPUT` 是发出远程过程调用的名称。 *rpcsrvname*是**sysname**，默认值为 **%** ，这是唯一返回结果集的值。  
  
`[ @publisher_type = ] 'publisher_type' OUTPUT` 是发布服务器的发布服务器类型。 *publisher_type*是**sysname**，默认值为 **%** ，这是唯一返回结果集的值。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**分发服务器**|**sysname**|分发服务器的名称。|  
|**分发数据库**|**sysname**|分发数据库的名称。|  
|**目录**|**nvarchar(255)**|工作目录的名称。|  
|**account**|**nvarchar(255)**|Windows 用户帐户的名称。|  
|**最小分发保持期**|**int**|最小分发保持期。|  
|**最大分发保持期**|**int**|最大分发保持期。|  
|**历史记录保持期**|**int**|历史记录保持期。|  
|**历史记录清除代理**|**nvarchar(100)**|历史记录清除代理的名称。|  
|**分发清除代理**|**nvarchar(100)**|分发清除代理的名称。|  
|**rpc 服务器名称**|**sysname**|远程分发服务器或本地分发服务器的名称。|  
|**rpc 登录名**|**sysname**|用于对远程分发服务器的远程过程调用的登录名。|  
|**发布服务器类型**|**sysname**|发布服务器的类型；可以为下列值之一：<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **ORACLE 网关**|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_helpdistributor**用于所有类型的复制。  
  
 如果在执行时指定一个或多个输出参数**sp_helpdistributor**、 设置为 NULL 的所有输出参数都分配值在退出和不返回任何结果集。 如果未指定输出参数，则返回结果集。  
  
## <a name="permissions"></a>权限  
 以下结果集列或输出参数返回到的成员**sysadmin**发布服务器上的固定的服务器角色和**db_owner**上对发布数据库的固定的数据库角色：  
  
|结果集列|输出参数|  
|-----------------------|----------------------|  
|account|**@account**|  
|min distrib retention|**@min_distretention**|  
|max distrib retention|**@max_distretention**|  
|history retention|**@history_retention**|  
|history cleanup agent|**@history_cleanupagent**|  
|distribution cleanup agent|**@distrib_cleanupagent**|  
|rpc login name|无|  
  
 以下结果集列返回给分发服务器上的某个发布的发布访问列表中的用户:  
  
-   directory  
  
 以下结果集列返回给所有用户。  
  
|结果集列|输出参数|  
|-----------------------|----------------------|  
|distributor|**@distributor**|  
|分发数据库 (distribution database)|**@distribdb**|  
|rpc server name|**@rpcsrvname**|  
|publisher type|**@publisher_type**|  
  
## <a name="see-also"></a>请参阅  
 [查看和修改分发服务器和发布服务器属性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
