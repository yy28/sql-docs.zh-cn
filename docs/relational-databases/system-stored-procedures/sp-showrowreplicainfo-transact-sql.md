---
title: sp_showrowreplicainfo (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_showrowreplicainfo_TSQL
- sp_showrowreplicainfo
helpviewer_keywords:
- sp_showrowreplicainfo
ms.assetid: 6a9dbc1a-e1e1-40c4-97cb-8164a2288f76
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5fdf29f59931c919b69b7c0662b2586d8df5ccc7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47791145"
---
# <a name="spshowrowreplicainfo-transact-sql"></a>sp_showrowreplicainfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  显示有关在合并复制中用作项目的表中的行的信息。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_showrowreplicainfo [ [ @ownername = ] 'ownername' ]  
    [ , [ @tablename =] 'tablename' ]   
        , [ @rowguid =] rowguid   
    [ , [ @show = ] 'show' ]   
```  
  
## <a name="arguments"></a>参数  
 [ **@ownername**=] **'***ownername*****  
 表所有者的名称。 *ownername*是**sysname**，默认值为 NULL。 如果数据库包含多个同名的表，但每个表具有不同的所有者，则该参数对于区分这些表很有用。  
  
 [  **@tablename =**] **'***tablename*****  
 包含所返回的信息行的表的名称。 *tablename*是**sysname**，默认值为 NULL。  
  
 [  **@rowguid =**] *rowguid*  
 行的唯一标识符。 *rowguid*是**uniqueidentifier**，无默认值。  
  
 [ **@show**=] **'***显示*****  
 确定要在结果集中返回的信息量。 *显示*是**nvarchar(20)** 这两者的默认值。 如果**行**，则返回仅行版本信息。 如果**列**，则返回仅列版本信息。 如果**同时**、 行和返回列信息。  
  
## <a name="result-sets-for-row-information"></a>行信息的结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|承载生成行版本项目的数据库的服务器名称。|  
|**db_name**|**sysname**|生成此项目的数据库的名称。|  
|**db_nickname**|**binary(6)**|生成此项目的数据库的别名。|  
|**version**|**int**|项的版本。|  
|**current_state**|**nvarchar(9)**|返回有关行的当前状态的信息。<br /><br /> **y** -行数据表示行的当前状态。<br /><br /> **n** -行数据不表示行的当前状态。<br /><br /> **\<n/a >** -不适用。<br /><br /> **\<未知 >** -无法确定当前状态。|  
|**rowversion_table**|**nchar(17)**|指示是否将行版本存储在[MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)表或[MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)表。|  
|**注释**|**nvarchar(255)**|有关此行版本项目的附加信息。 通常，该字段为空。|  
  
## <a name="result-sets-for-column-information"></a>列信息的结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|承载生成列版本项目的数据库的服务器名称。|  
|**db_name**|**sysname**|生成此项目的数据库的名称。|  
|**db_nickname**|**binary(6)**|生成此项目的数据库的别名。|  
|**version**|**int**|项的版本。|  
|**colname**|**sysname**|列版本项目表示的项目列的名称。|  
|**注释**|**nvarchar(255)**|有关此列版本项目的附加信息。 通常，该字段为空。|  
  
## <a name="result-set-for-both"></a>行信息和列信息的结果集  
 如果该值**两者**为选择*显示*，则返回的行和列结果集。  
  
## <a name="remarks"></a>备注  
 **sp_showrowreplicainfo**合并复制中使用。  
  
## <a name="permissions"></a>Permissions  
 **sp_showrowreplicainfo**的成员只可以执行**db_owner**固定的数据库角色的发布数据库上或通过发布访问列表 (PAL) 的发布数据库上的成员。  
  
## <a name="see-also"></a>请参阅  
 [检测和解决合并复制冲突](../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
