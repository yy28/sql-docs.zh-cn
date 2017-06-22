---
title: MSSQLSERVER_41333 | Microsoft Docs
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
- 41333 (Database Engine error)
ms.assetid: c3c3ae9a-1e4c-4de6-ba72-2f393375b053
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 72f5461f4e60b7e4c5cb53df75906d1aae0a07a5
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver41333"></a>MSSQLSERVER_41333
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|41333|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|CROSS_CONTAINER_ISOLATION_FAILURE|  
|消息正文|以下事务必须在快照隔离下访问内存优化表和本机编译存储过程：RepeatableRead 事务、Serializable 事务以及在 RepeatableRead 或 Serializable 隔离中访问非内存优化表的事务。|  
  
## <a name="explanation"></a>解释  
对于基于磁盘的事务和 XTP 事务之间的更高隔离级别用户，存在一些限制。  
  
## <a name="user-action"></a>用户操作  
不要尝试对内存优化表（和本机编译存储过程）以及基于磁盘的表执行高级别隔离操作。  
  
有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另请参阅  
[内存中 OLTP（内存中优化）](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  

