---
title: 停止跟踪 （SQL Server 事件探查器） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], stopping
- stopping traces
ms.assetid: 47c4f33d-63e0-4444-bec8-4c1c91f8e25c
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fd1b3b36f58d3f8deb31fd4ddff477f6590321f2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128214"
---
# <a name="stop-a-trace-sql-server-profiler"></a>停止跟踪 (SQL Server Profiler)
  本主题介绍如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]停止正在运行的跟踪。  
  
 停止跟踪将停止捕获数据。 停止跟踪后，除非已将数据捕获到了跟踪文件或跟踪表中，否则重新启动该跟踪将丢失以前捕获的数据。 您还可以在停止跟踪后将收集的数据保存到表或文件。 当停止跟踪时，以前选择的所有跟踪属性将保留， 您也可以更改名称、事件、列和筛选器。  
  
### <a name="to-stop-a-trace"></a>停止跟踪  
  
1.  选择正在运行的跟踪。  
  
2.  在 **“文件”** 菜单上，单击 **“停止跟踪”**。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 事件探查器](sql-server-profiler.md)  
  
  