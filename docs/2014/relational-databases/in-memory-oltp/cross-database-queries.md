---
title: 跨数据库查询 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a0305f5b-91bd-4d18-a2fc-ec235b062fd3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d8739a95f0676adfdbc890512aeb5246565bacdb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63071585"
---
# <a name="cross-database-queries"></a>跨数据库查询
  在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 中，内存优化表不支持跨数据库事务。 不能从也访问某一内存优化表的相同事务或相同查询访问其他数据库。 可以轻松地将来自一个数据库的某个表中的数据复制到其他数据库的内存优化表中。  
  
 表变量不是事务性的。 因此，内存优化表变量可用于跨数据库查询中，并因此可以简化将数据从一个数据库中移到另一个数据库的内存优化表中的操作。 可以使用两个事务。 在第一个事务中，将数据从远程表插入到变量中。 在第二个事务中，将数据从变量插入到本地内存优化表中。  
  
 例如，若要使用 dbo.tt1 类型的变量@v1 ，从数据库 db1 中的表 t1 将行复制到 db2 中的表 t2，你可以使用类似于下面的内容：  
  
```sql  
USE db2   
GO   
DECLARE @v1 dbo.tt1   
INSERT @v1 SELECT * FROM db1.dbo.t1   
INSERT dbo.t2 SELECT * FROM @v1   
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [迁移到内存中 OLTP](migrating-to-in-memory-oltp.md)  
  
  
