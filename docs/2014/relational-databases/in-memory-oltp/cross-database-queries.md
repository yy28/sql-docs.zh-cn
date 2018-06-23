---
title: 跨数据库查询 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a0305f5b-91bd-4d18-a2fc-ec235b062fd3
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: dd86d3e1c67cb1a87690919a6d9336a434d14954
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018440"
---
# <a name="cross-database-queries"></a>跨数据库查询
  在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 中，内存优化表不支持跨数据库事务。 不能从也访问某一内存优化表的相同事务或相同查询访问其他数据库。 可以轻松地将来自一个数据库的某个表中的数据复制到其他数据库的内存优化表中。  
  
 表变量不是事务性的。 因此，内存优化表变量可用于跨数据库查询中，并因此可以简化将数据从一个数据库中移到另一个数据库的内存优化表中的操作。 可以使用两个事务。 在第一个事务中，将数据从远程表插入到变量中。 在第二个事务中，将数据从变量插入到本地内存优化表中。  
  
 例如，若要复制的行从数据库 db1 中的表 t1 的表 t2 中 db2，到使用变量@v1类型 dbo.tt1，您可以使用类似于：  
  
```tsql  
USE db2   
GO   
DECLARE @v1 dbo.tt1   
INSERT @v1 SELECT * FROM db1.dbo.t1   
INSERT dbo.t2 SELECT * FROM @v1   
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [迁移到内存中 OLTP](migrating-to-in-memory-oltp.md)  
  
  