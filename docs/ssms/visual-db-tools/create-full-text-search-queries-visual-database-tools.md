---
description: 创建全文搜索查询 (Visual Database Tools)
title: 创建全文搜索查询
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- CONTAINS predicate (Transact-SQL)
- queries [full-text search], creating
- full-text queries [SQL Server], creating
ms.assetid: 537fa556-390e-4c88-9b8e-679848d94abc
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: b861cf926bdbc43fda8986be44dacb5652196b7a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88369893"
---
# <a name="create-full-text-search-queries-visual-database-tools"></a>创建全文搜索查询 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
全文搜索使用 CONTAINS 谓词来查找在给定列中包含指定文本的行。 全文搜索仅适用于具有活动的全文索引的列。 如果试图将 CONTAINS 子句用于不具有当前活动的全文索引的列，则将收到错误。 有关全文检索和 CONTAINS 子句的详细信息，请参阅 [全文搜索 (SQL Server)](../../relational-databases/search/full-text-search.md) 和 [CONTAINS (Transact-SQL)](https://msdn.microsoft.com/996c72fc-b1ab-4c96-bd12-946be9c18f84)。  
  
### <a name="to-create-a-full-text-search-query"></a>创建全文搜索查询  
  
1.  在解决方案资源管理器中打开一个查询或创建新的查询。  
  
2.  在该查询的 WHERE 子句中，用 CONTAINS 函数来搜索全文本列。  
  
## <a name="see-also"></a>另请参阅  
[支持的查询类型 (Visual Database Tools)](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[执行基本的查询操作 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
