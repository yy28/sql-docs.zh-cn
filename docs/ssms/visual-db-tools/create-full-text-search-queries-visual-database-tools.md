---
title: "创建全文搜索查询 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CONTAINS predicate (Transact-SQL)
- queries [full-text search], creating
- full-text queries [SQL Server], creating
ms.assetid: 537fa556-390e-4c88-9b8e-679848d94abc
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3c7f13f234c595c494e22a1bb0888899a40df51b
ms.lasthandoff: 04/11/2017

---
# <a name="create-full-text-search-queries-visual-database-tools"></a>创建全文搜索查询 (Visual Database Tools)
全文搜索使用 CONTAINS 谓词来查找在给定列中包含指定文本的行。 全文搜索仅适用于具有活动的全文索引的列。 如果试图将 CONTAINS 子句用于不具有当前活动的全文索引的列，则将收到错误。 有关全文检索和 CONTAINS 子句的详细信息，请参阅 [全文搜索 (SQL Server)](http://msdn.microsoft.com/en-us/a0ce315d-f96d-4e5d-b4eb-ff76811cab75) 和 [CONTAINS (Transact-SQL)](http://msdn.microsoft.com/en-us/996c72fc-b1ab-4c96-bd12-946be9c18f84)。  
  
### <a name="to-create-a-full-text-search-query"></a>创建全文搜索查询  
  
1.  在解决方案资源管理器中打开一个查询或创建新的查询。  
  
2.  在该查询的 WHERE 子句中，用 CONTAINS 函数来搜索全文本列。  
  
## <a name="see-also"></a>另请参阅  
[支持的查询类型 (Visual Database Tools)](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[执行基本的查询操作 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  

