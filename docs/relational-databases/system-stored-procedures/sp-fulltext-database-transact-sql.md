---
title: sp_fulltext_database (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_fulltext_database_TSQL
- sp_fulltext_database
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_database
ms.assetid: eeb1e151-eb00-484c-8fd1-5641e621ffc6
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8f4904de1142052a8286aabb4a69bf439871b84e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33241459"
---
# <a name="spfulltextdatabase-transact-sql"></a>sp_fulltext_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  对 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更高版本中的全文目录没有影响，支持它只是为了向后兼容。 **sp_fulltext_database**不会禁用给定数据库的全文引擎。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，所有用户创建的数据库始终启用全文索引。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]使用[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_fulltext_database [@action=] 'action'  
```  
  
## <a name="arguments"></a>参数  
 [  **@action=**] *****操作*****  
 要执行的操作。 **操作**是**varchar （20)**，并且可以为这些值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|**enable**|支持它仅仅是为了保持向后兼容。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更高版本中对全文目录无效。|  
|**disable**|支持它仅仅是为了保持向后兼容。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更高版本中对全文目录无效。|  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更高版本中，无法禁用全文索引。 禁用全文索引不会删除从行**sysfulltextcatalogs**并且不表示全文索引已启用的表不再标记为全文索引。 所有的全文元数据定义仍然在系统表中。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色和**db_owner**固定的数据库角色可以执行**sp_fulltext_database**。  
  
## <a name="see-also"></a>另请参阅  
 [DATABASEPROPERTYEX (Transact-SQL)](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [FULLTEXTSERVICEPROPERTY (Transact-SQL)](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
