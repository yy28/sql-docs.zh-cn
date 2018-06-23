---
title: SQL Server Profiler-性能计数器限制 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.pro.performancecounterlimit.f1
helpviewer_keywords:
- Performance Counters List dialog box
ms.assetid: d10140ef-36c4-449c-b365-1cff1b2524e4
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2548fbd28af45cbd888a183a739362f0e7767218
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026191"
---
# <a name="sql-server-profiler---performance-counters-limit"></a>SQL Server Profiler - 性能计数器限制
  使用“性能计数器限制”对话框可以在将系统监视器性能日志文件与 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 跟踪关联时限制该文件中的信息。 对于相应的关联，您可以使用此对话框选择应该显示和使用的计数器。  
  
 **“性能计数器限制”** 对话框填充有性能日志文件所包含的性能对象和计数器。  
  
### <a name="to-select-performance-objects-and-counters-to-correlate-with-a-trace"></a>选择要与跟踪关联的性能对象和计数器  
  
1.  展开性能对象以查看性能日志文件中包含的计数器。  
  
2.  选中要与 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 跟踪文件关联的计数器。  
  
     如果希望选择某个性能对象的所有计数器，请选中与该性能对象相邻的框。 如果选中指示计算机的最顶层节点，则会选择性能日志文件中包含的所有性能对象和计数器。  
  
## <a name="see-also"></a>请参阅  
 [将跟踪与 Windows 性能日志数据关联 (SQL Server Profiler)](../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data.md)  
  
  