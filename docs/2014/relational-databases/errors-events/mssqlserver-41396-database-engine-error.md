---
title: MSSQLSERVER_41396 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41396 (Database Engine error)
ms.assetid: 4ff04042-8367-46f3-8a16-c94682d6eedb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f66a0ce65a0d16099d7371c003a813b129b3859f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62867871"
---
# <a name="mssqlserver_41396"></a>MSSQLSERVER_41396
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|41396|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|MAX_SORT_ROWS_EXCEEDED|  
|消息正文|该排序操作超出了缓冲区限制。 存储过程执行已中止。 有关详细信息，请查阅 SQL Server 联机丛书。|  
  
## <a name="explanation"></a>说明  
 本机编译的存储过程在内存中执行排序操作。 对排序缓冲区的大小存在限制。 此错误意味着该排序缓冲区的大小超过了此限制。 排序操作和存储过程执行已中止。  
  
 排序缓冲区中每一行或条目的大小由已排序的行数以及查询中联接的数目和聚合函数的数目和类型确定。 通过简化查询，可以减小每一行的大小，从而在排序缓冲区中容纳更多的行。 基表中行的大小不会影响排序缓冲区中每一行或条目的大小。  
  
## <a name="user-action"></a>用户操作  
 选择更少的行，或者通过删除联接或聚合函数降低查询的复杂程度。  
  
## <a name="see-also"></a>另请参阅  
 [内存中 OLTP（内存中优化）](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
