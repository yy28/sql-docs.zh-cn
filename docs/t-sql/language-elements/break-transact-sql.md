---
title: "中断 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BREAK
- BREAK_TSQL
dev_langs: TSQL
helpviewer_keywords:
- exiting innermost loop [SQL Server]
- END keyword
- ignored statements
- BREAK keyword
ms.assetid: 67c30b8d-3f15-41ad-b9a9-a4ced3b2af9f
caps.latest.revision: "34"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7f37cdbfaf61ff29137348743d44216de7801879
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="break-transact-sql"></a>BREAK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  退出 WHILE 循环内部的 WHILE 语句或 IF ELSE 语句最里面的循环。 将执行出现在 END 关键字后面的任何语句，END 关键字为循环结束标记。 IF 测试通常会启动 BREAK，但并不总是如此。  
  
## <a name="examples"></a>示例  
  
```  
-- Uses AdventureWorks  
  
WHILE ((SELECT AVG(ListPrice) FROM dbo.DimProduct) < $300)  
BEGIN  
    UPDATE DimProduct  
        SET ListPrice = ListPrice * 2;  
     IF ((SELECT MAX(ListPrice) FROM dbo.DimProduct) > $500)  
         BREAK;  
END  
```  
  
## <a name="see-also"></a>另请参阅  
 [控制流语言 &#40;Transact SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [虽然 &#40;Transact SQL &#41;](../../t-sql/language-elements/while-transact-sql.md)   
 [IF...ELSE (Transact-SQL)](../../t-sql/language-elements/if-else-transact-sql.md)  
  
  


