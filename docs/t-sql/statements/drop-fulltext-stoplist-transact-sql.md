---
title: "DROP FULLTEXT STOPLIST (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_FULLTEXT_STOPLIST_TSQL
- DROP FULLTEXT STOPLIST
dev_langs:
- TSQL
helpviewer_keywords:
- DROP FULLTEXT STOPLIST statement
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 3ee2a2bb-1dfb-4e7c-90e9-9d917cd84a15
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 86431229e26091e2fde6c3f81873523c5f09de68
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="drop-fulltext-stoplist-transact-sql"></a>DROP FULLTEXT STOPLIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的数据库中删除全文非索引字表。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
> [!IMPORTANT]  
>  只有在兼容级别为 100 或更高时，才支持 CREATE FULLTEXT STOPLIST。 在 80 和 90 兼容级别下，会始终为数据库分配系统非索引字表。  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP FULLTEXT STOPLIST stoplist_name  
;  
```  
  
## <a name="arguments"></a>参数  
 *stoplist_name*  
 要从数据库中删除的全文本非索引字表的名称。  
  
## <a name="remarks"></a>注释  
 如果有任何全文索引引用了已删除的全文本非索引字表，则 DROP FULLTEXT STOPLIST 会失败。  
  
## <a name="permissions"></a>Permissions  
 若要删除非索引字表，需要具有删除权限的非索引字表或中的成员身份**db_owner**或**db_ddladmin**固定数据库角色的成员。  
  
## <a name="examples"></a>示例  
 下面的示例将删除名为 `myStoplist` 的全文非索引字表。  
  
```  
DROP FULLTEXT STOPLIST myStoplist;  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER FULLTEXT STOPLIST &#40;Transact SQL &#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)   
 [创建全文非索引字表 &#40;Transact SQL &#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [sys.fulltext_stoplists &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)  
  
  

