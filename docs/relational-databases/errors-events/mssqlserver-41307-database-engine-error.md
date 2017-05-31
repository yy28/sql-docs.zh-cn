---
title: MSSQLSERVER_41307 | Microsoft Docs
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
- 41307 (Database Engine error)
ms.assetid: 56f56410-b07d-4379-b01c-702c95761070
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f0b0096029fd86def5eb2f44bdba4dcea418137c
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver41307"></a>MSSQLSERVER_41307
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|41307|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|HK_HEKATON_ROW_LIMIT|  
|消息正文|已超出了内存优化表 *number* 字节的行大小限制。 请简化表定义。|  
  
## <a name="explanation"></a>解释  
内存优化表的行大小限制为 8,060 字节。 有关详细信息，请参阅 [内存优化表中的表和行大小](~/relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)。 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另请参阅  
[内存中 OLTP（内存中优化）](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  

