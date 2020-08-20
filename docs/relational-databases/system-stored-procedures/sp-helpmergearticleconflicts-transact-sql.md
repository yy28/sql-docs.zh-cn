---
description: sp_helpmergearticleconflicts (Transact-SQL)
title: sp_helpmergearticleconflicts (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergearticleconflicts
- sp_helpmergearticleconflicts_TSQL
helpviewer_keywords:
- sp_helpmergearticleconflicts
ms.assetid: 4678a2b9-9a5f-4193-a20d-2e11fc896c3a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9a2e2272713266ea0dbae5d4bc8da76bff87b919
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474049"
---
# <a name="sp_helpmergearticleconflicts-transact-sql"></a>sp_helpmergearticleconflicts (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  返回发布中有冲突的项目。 此存储过程在发布服务器上针对发布数据库执行，或在订阅服务器上针对合并订阅数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpmergearticleconflicts [ [ @publication = ] 'publication' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publsher_db' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'` 合并发布的名称。*发布* 的数据类型为 **sysname**，默认值为 **%** ，它返回数据库中具有冲突的所有项目。  
  
`[ @publisher = ] 'publisher'` 发布服务器的名称。*发布服务器* 的 **sysname**，默认值为 NULL。  
  
`[ @publisher_db = ] 'publisher_db'` 发布服务器数据库的名称。*publisher_db* 的默认值为 **sysname**，默认值为 NULL。  
  
## <a name="result-sets"></a>结果集  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**文章**|**sysname**|项目的名称。|  
|**source_owner**|**sysname**|源对象的所有者。|  
|**source_object**|**nvarchar (386) **|源对象的名称。|  
|**conflict_table**|**nvarchar(258)**|存储插入或更新冲突的表的名称。|  
|**guidcolname**|**sysname**|源对象的 RowGuidCol 名称。|  
|**centralized_conflicts**|**int**|冲突记录是否存储在给定发布服务器上。|  
  
 如果项目只包含删除冲突并且没有 **conflict_table** 的行，则结果集中 **conflict_table** 的名称为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** (成功) 或 **1** (失败)   
  
## <a name="remarks"></a>备注  
 **sp_helpmergearticleconflicts** 用于合并复制。  
  
## <a name="permissions"></a>权限  
 只有 **sysadmin** 固定服务器角色的成员和 **db_owner** 固定数据库角色的成员才能执行 **sp_helpmergearticleconflicts**。  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
