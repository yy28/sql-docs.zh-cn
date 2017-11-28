---
title: "删除搜索属性列表 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_SEARCH_PROPERTY_LIST_TSQL
- DROP SEARCH PROPERTY LIST
dev_langs: TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- DROP SEARCH PROPERTY LIST statement
- search property lists [SQL Server], dropping
- search property lists [SQL Server], deleting
ms.assetid: 7c7ce52a-6b77-4a1c-9abf-d5feb664bea8
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 94a86720e49809e56aefeef1b3264c511f30f6be
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="drop-search-property-list-transact-sql"></a>DROP SEARCH PROPERTY LIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  如果搜索属性列表当前与当前数据库中的任何全文检索均不关联，则从数据库中删除属性列表。  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP SEARCH PROPERTY LIST property_list_name  
;  
```  
  
## <a name="arguments"></a>参数  
 *property_list_name*  
 要删除的搜索属性列表的名称。 *property_list_name*是一个标识符。  
  
 若要查看现有的属性列表的名称，请使用[sys.registered_search_property_lists](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)目录视图，，如下所示：  
  
```  
SELECT name FROM sys.registered_search_property_lists;  
```  
  
## <a name="remarks"></a>注释  
 当搜索属性列表与任何全文检索关联时，无法从数据库中删除该列表。 若要从给定的全文索引中删除搜索属性列表，请使用[ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md)语句，并使用关闭指定 SET SEARCH PROPERTY LIST 子句或另一个名称搜索属性列表。  
  
 **若要查看的属性列表上的服务器实例**  
  
-   [sys.registered_search_property_lists (Transact-SQL)](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
 **若要查看的属性列表与全文索引相关联**  
  
-   [sys.fulltext_indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
  
 **若要删除的全文索引的属性列表**  
  
-   [ALTER FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
##  <a name="Permissions"></a> 权限  
 要求具有搜索属性列表的 CONTROL 权限。  
  
> [!NOTE]  
>  属性列表所有者可以授予列表的 CONTROL 权限。 默认情况下，创建搜索属性列表的用户就是其所有者。 可以通过更改所有者[ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]语句。  
  
## <a name="examples"></a>示例  
 以下示例从 `JobCandidateProperties` 数据库中删除 `AdventureWorks2012` 属性列表。  
  
```  
DROP SEARCH PROPERTY LIST JobCandidateProperties;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER SEARCH PROPERTY LIST &#40;Transact SQL &#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)   
 [创建搜索属性列表 &#40;Transact SQL &#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)   
 [使用搜索属性列表搜索文档属性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.registered_search_properties &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [sys.registered_search_property_lists &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [sys.registered_search_property_lists (Transact-SQL)](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
  
