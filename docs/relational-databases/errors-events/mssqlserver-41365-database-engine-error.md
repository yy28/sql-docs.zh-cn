---
title: MSSQLSERVER_41365 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 41365 (Database Engine error)
ms.assetid: 4fc7ec15-b722-4e3d-b7f9-3d39d171e96e
caps.latest.revision: "7"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: a74c259a854e5db28c29c58d1b7101c191a00177
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver41365"></a>MSSQLSERVER_41365
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|41365|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|HK_MERGE_SCHEDULE_ERROR|  
|消息正文|未计划数据库 %.*ls 事务范围 [%ld，%ld] 的合并要求。 表示范围的检查点文件对合并不可用或是正在进行的合并的一部分。|  
  
## <a name="explanation"></a>解释  
表示范围的检查点文件对合并不可用或是正在进行的合并的一部分。  
  
## <a name="user-action"></a>用户操作  
为合并提供更好的事务范围/等待，然后再次发出同一请求。 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另请参阅  
[内存中 OLTP（内存中优化）](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
