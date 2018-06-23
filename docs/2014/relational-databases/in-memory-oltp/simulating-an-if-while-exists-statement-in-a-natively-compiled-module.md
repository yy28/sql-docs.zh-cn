---
title: 模拟 EXISTS 子句在本机编译的存储过程 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c0e187c1-cbd9-463c-b417-8a734574f102
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: 68515c717fa39cfd626c83625dc7b95c24c68d69
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028577"
---
# <a name="simulating-an-exists-clause-in-a-natively-compiled-stored-procedure"></a>在本机编译的存储过程中模拟 EXISTS 子句
  本机编译的存储过程不支持 `EXISTS` 子句，但是可以解决这个问题：  
  
```tsql  
DECLARE @exists BIT = 0  
SELECT TOP 1 @exists = 1 FROM MyTable WHERE …  
IF @exists = 1  
```  
  
## <a name="see-also"></a>请参阅  
 [本机编译的存储过程的迁移问题](migration-issues-for-natively-compiled-stored-procedures.md)   
 [内存中 OLTP 不支持的 Transact-SQL 构造](transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  