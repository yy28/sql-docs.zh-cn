---
title: MSSQLSERVER_1904 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 1904 (Database Engine error)
ms.assetid: 2a35d57d-74e2-45a2-8f67-3f2e51d69712
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7f40d48806c181cc12c804bfa5fdf9796f83b77e
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver1904"></a>MSSQLSERVER_1904
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1904|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|KEYCOUNT|  
|消息正文|表 '%.\*ls' 的 %S_MSG '%.*ls' 在 %S_MSG 键列表中具有 %d 个列名。 索引或统计信息键列列表的最大限制为 %d。|  
  
## <a name="explanation"></a>解释  
指定索引或统计信息的键列列表超出了允许的最大列数。  
  
## <a name="user-action"></a>用户操作  
修改键列的列表，使其中包含的列数小于指定的最大列数。  
  
对于非聚集索引，请考虑使用 CREATE INDEX 语句中的 INCLUDE 子句，将列作为非键列添加到索引中。 使用此方法可避免超过当前的索引大小限值（即最多 16 个键列）。 有关详细信息，请参阅 [Create Indexes with Included Columns](~/relational-databases/indexes/create-indexes-with-included-columns.md)。  
  
## <a name="see-also"></a>另请参阅  
[CREATE INDEX (Transact-SQL)](~/t-sql/statements/create-index-transact-sql.md)  
[CREATE STATISTICS (Transact-SQL)](~/t-sql/statements/create-statistics-transact-sql.md)  
  

