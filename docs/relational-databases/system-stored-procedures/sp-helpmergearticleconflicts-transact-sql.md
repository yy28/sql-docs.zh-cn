---
title: sp_helpmergearticleconflicts (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergearticleconflicts
- sp_helpmergearticleconflicts_TSQL
helpviewer_keywords:
- sp_helpmergearticleconflicts
ms.assetid: 4678a2b9-9a5f-4193-a20d-2e11fc896c3a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 47a49e5d2c6faad6be65bc93b0151b6ab8d85fc6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47759245"
---
# <a name="sphelpmergearticleconflicts-transact-sql"></a>sp_helpmergearticleconflicts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回发布中有冲突的项目。 此存储过程在发布服务器上针对发布数据库执行，或在订阅服务器上针对合并订阅数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpmergearticleconflicts [ [ @publication = ] 'publication' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publsher_db' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication=**] **'***publication***'**  
 是合并发布的名称。*出版物*是**sysname**，默认值为**%**，这会返回数据库中有冲突的所有项目。  
  
 [ **@publisher=**] **'***publisher***'**  
 是发布服务器的名称。*发布服务器*是**sysname**，默认值为 NULL。  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 是发布服务器数据库的名称。*publisher_db*是**sysname**，默认值为 NULL。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**article**|**sysname**|项目的名称。|  
|**source_owner**|**sysname**|源对象的所有者。|  
|**source_object**|**nvarchar(386)**|源对象的名称。|  
|**conflict_table**|**nvarchar(258)**|存储插入或更新冲突的表的名称。|  
|**guidcolname**|**sysname**|源对象的 RowGuidCol 名称。|  
|**centralized_conflicts**|**int**|冲突记录是否存储在给定发布服务器上。|  
  
 如果将项目的唯一删除冲突而没有**conflict_table**行的名称**conflict_table**结果集为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_helpmergearticleconflicts**合并复制中使用。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色和**db_owner**固定的数据库角色可以执行**sp_helpmergearticleconflicts**。  
  
## <a name="see-also"></a>请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
