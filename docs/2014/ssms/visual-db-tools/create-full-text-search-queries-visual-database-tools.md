---
title: 创建全文搜索查询 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- CONTAINS predicate (Transact-SQL)
- queries [full-text search], creating
- full-text queries [SQL Server], creating
ms.assetid: 537fa556-390e-4c88-9b8e-679848d94abc
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3963876ce326529fd2538adc2d303d218406a924
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026924"
---
# <a name="create-full-text-search-queries-visual-database-tools"></a>创建全文搜索查询 (Visual Database Tools)
  全文搜索使用 CONTAINS 谓词来查找在给定列中包含指定文本的行。 全文搜索仅适用于具有活动的全文索引的列。 如果试图将 CONTAINS 子句用于不具有当前活动的全文索引的列，则将收到错误。 全文索引和 CONTAINS 子句的详细信息，请参阅[的全文搜索](../../relational-databases/search/full-text-search.md)和[CONTAINS &#40;TRANSACT-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)。  
  
### <a name="to-create-a-full-text-search-query"></a>创建全文搜索查询  
  
1.  在解决方案资源管理器中打开一个查询或创建新的查询。  
  
2.  在该查询的 WHERE 子句中，用 CONTAINS 函数来搜索全文本列。  
  
## <a name="see-also"></a>请参阅  
 [支持的查询类型&#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [设计查询和视图的操作指南主题&#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [执行基本的查询操作 (Visual Database Tools)](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
