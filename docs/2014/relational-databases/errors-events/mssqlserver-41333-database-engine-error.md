---
title: MSSQLSERVER_41333 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41333 (Database Engine error)
ms.assetid: c3c3ae9a-1e4c-4de6-ba72-2f393375b053
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0fdc950e523fe1851aaf5664e2d40ff311a24ab7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85032990"
---
# <a name="mssqlserver_41333"></a>MSSQLSERVER_41333
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|41333|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|CROSS_CONTAINER_ISOLATION_FAILURE|  
|消息正文|以下事务必须在快照隔离下访问内存优化表和本机编译存储过程：RepeatableRead 事务、Serializable 事务以及在 RepeatableRead 或 Serializable 隔离中访问非内存优化表的事务。|  
  
## <a name="explanation"></a>说明  
 对于基于磁盘的事务和 XTP 事务之间的更高隔离级别用户，存在一些限制。  
  
## <a name="user-action"></a>用户操作  
 不要尝试对内存优化表（和本机编译存储过程）以及基于磁盘的表执行高级别隔离操作。  
  
 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另请参阅  
 [内存中 OLTP（内存中优化）](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
