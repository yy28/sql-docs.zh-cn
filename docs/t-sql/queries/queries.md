---
title: 查询 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5ff02a32-e8d3-479c-ae8b-07581e41f5f8
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4c1757061889691f01ed07d5a2a0d4b9124701cd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="queries"></a>查询
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  数据操作语言 (DML) 是用于检索和使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 和 SQL 数据库中的数据的词汇。 大部分也可在 SQL 数据仓库和 PDW 中使用（请查看各语句了解详细信息）。 使用这些语句可以从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库添加、修改、查询或删除数据。  
  
## <a name="in-this-section"></a>本节内容  
 下表列出了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的 DML 语句。  
  
|||  
|-|-|  
|[BULK INSERT (Transact-SQL)](../../t-sql/statements/bulk-insert-transact-sql.md)|[SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)|  
|[DELETE (Transact-SQL)](../../t-sql/statements/delete-transact-sql.md)|[UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)|  
|[INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)|[UPDATETEXT (Transact-SQL)](../../t-sql/queries/updatetext-transact-sql.md)|  
|[MERGE (Transact-SQL)](../../t-sql/statements/merge-transact-sql.md)|[WRITETEXT (Transact-SQL)](../../t-sql/queries/writetext-transact-sql.md)|  
|[READTEXT (Transact-SQL)](../../t-sql/queries/readtext-transact-sql.md)||  
  
 下表列出了在多个 DML 语句或子句中使用的子句。  
  
|子句|可用于的语句|  
|------------|-------------------------------------|  
|[FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)|DELETE、SELECT、UPDATE|  
|[提示 (Transact-SQL)](../../t-sql/queries/hints-transact-sql.md)|DELETE、INSERT、SELECT、UPDATE|  
|[OPTION 子句 (Transact-SQL)](../../t-sql/queries/option-clause-transact-sql.md)|DELETE、SELECT、UPDATE|  
|[OUTPUT 子句 (Transact-SQL)](../../t-sql/queries/output-clause-transact-sql.md)|DELETE、INSERT、MERGE、UPDATE|  
|[搜索条件 (Transact-SQL)](../../t-sql/queries/search-condition-transact-sql.md)|DELETE、MERGE、SELECT、UPDATE|  
|[表值构造函数 (Transact-SQL)](../../t-sql/queries/table-value-constructor-transact-sql.md)|FROM、INSERT、MERGE|  
|[TOP (Transact-SQL)](../../t-sql/queries/top-transact-sql.md)|DELETE、INSERT、MERGE、SELECT、UPDATE|  
|[WHERE (Transact-SQL)](../../t-sql/queries/where-transact-sql.md)|DELETE、SELECT、UPDATE、MATCH|  
|[WITH common_table_expression (Transact-SQL)](../../t-sql/queries/with-common-table-expression-transact-sql.md)|DELETE、INSERT、MERGE、SELECT、UPDATE|  
  
  
