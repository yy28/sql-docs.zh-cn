---
title: “性能”事件类别 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
topic_type:
- apiref
helpviewer_keywords:
- SQL Server event classes, Performance event category
- Performance event category [SQL Server]
- event classes [SQL Server], Performance event category
ms.assetid: 708f3585-d8be-4980-bbff-672d7c59397e
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 35b8a30db1271f393b9252ed4088a4d628cd4f1e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025203"
---
# <a name="performance-event-category"></a>Performance 事件类别
  使用 **Performance** 事件类别可以监视 **Showplan** 事件类以及在执行 SQL 数据操作语言 (DML) 运算符时生成的事件类。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[Auto Stats 事件类](auto-stats-event-class.md)|指示已自动更新索引统计信息和列统计信息。|  
|[Degree of Parallelism (7.0 Insert) 事件类](degree-of-parallelism-7-0-insert-event-class.md)|指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已经使用串行或并行计划执行 SELECT、INSERT、UPDATE 或 DELETE 语句。 此外，还会报告用来执行该操作的 CPU 数。|  
|[Performance Statistics 事件类](performance-statistics-event-class.md)|监视正在执行的查询的性能。|  
|[Showplan All 事件类](showplan-all-event-class.md)|标识 SQL 语句中的 **Showplan** 运算符。|  
|[Showplan All for Query Compile 事件类](showplan-all-for-query-compile-event-class.md)|显示 **Showplan** 运算符的编写时数据。|  
|[Showplan Statistics Profile 事件类](showplan-statistics-profile-event-class.md)|显示查询的估计开销。|  
|[Showplan XML 事件类](showplan-xml-event-class.md)|标识 SQL 语句中的 **Showplan** 运算符。 该事件类将每个事件作为定义好的 XML 文档进行存储。|  
|[Showplan XML For Query Compile 事件类](showplan-xml-for-query-compile-event-class.md)|以 XML 格式显示 **Showplan** 运算符的编写时数据。|  
|[Showplan XML Statistics Profile 事件类](showplan-xml-statistics-profile-event-class.md)|标识与 SQL 语句关联的 **Showplan** 运算符。 将输出一个 XML 文档。|  
|[SQL:FullTextQuery 事件类](sql-fulltextquery-event-class.md)|指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已执行全文查询。|  
|[Plan Guide Successful 事件类](plan-guide-successful-event-class.md)|指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已成功为计划指南中包含的查询或批处理生成执行计划。|  
|[Plan Guide Unsuccessful 事件类](plan-guide-unsuccessful-event-class.md)|指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法为计划指南中包含的查询或批处理生成执行计划。|  
  
## <a name="see-also"></a>请参阅  
 [扩展事件](../extended-events/extended-events.md)  
  
  