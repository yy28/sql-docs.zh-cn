---
title: ORDER BY 子句中的列别名不能以表别名作为前缀 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- aliases [SQL Server], columns
ms.assetid: fee7328f-6e8d-4005-930b-56fb6f17e0b2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1f4328c6a70c00766979a13bbcf8dc2b8bd77f42
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66096321"
---
# <a name="column-aliases-in-order-by-clause-cannot-be-prefixed-by-table-alias"></a>ORDER BY 子句中的列别名不能以表别名作为前缀
  在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本中，ORDER BY 子句中的列别名不能以表别名作为前缀。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
 例如，以下查询可在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中正常执行，而在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中却返回错误。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT FirstName AS f, LastName AS l  
FROM Person.Contact p  
ORDER BY p.l  
```  
  
 
  [!INCLUDE[ssDEversion10](../../includes/ssdeversion10-md.md)] 不会将 `p.l` 子句中的 `ORDER BY` 与表中的某个有效列匹配。  
  
### <a name="exception"></a>异常  
 如果 ORDER BY 子句中指定的带有前缀的列别名在指定的表中是有效的列名，则该查询在执行时不会出错；在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，该语句的语义可能有所不同。 例如，下面的语句中指定的列别名 (`id`) 在 `sysobjects` 表中是有效的列名。 在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中执行该语句时，对结果集排序之后将执行 `CAST` 操作。 也就是说，在排序操作中使用了 `name` 列。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中，`CAST` 操作是在排序操作之前执行的。 也就是说，在排序操作中使用了表中的 `id` 列，并以意外顺序返回了结果集。  
  
```  
SELECT CAST (o.name AS char(128)) AS id  
FROM sysobjects AS o  
ORDER BY o.id;  
```  
  
## <a name="corrective-action"></a>纠正措施  
 可通过下面两种方式之一修改在 ORDER BY 子句中将表别名作为列别名前缀的查询：  
  
-   尽量不要对 ORDER BY 子句中的列别名加前缀。  
  
-   用列名替换列别名。  
  
 例如，下面这两个查询在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中执行时均不会出错：  
  
```  
USE AdventureWorks2012;  
GO  
SELECT FirstName AS f, LastName AS l  
FROM Person.Contact p  
ORDER BY l  
  
USE AdventureWorks2012;  
GO  
SELECT FirstName AS f, LastName AS l  
FROM Person.Contact p  
ORDER BY p.LastName  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
