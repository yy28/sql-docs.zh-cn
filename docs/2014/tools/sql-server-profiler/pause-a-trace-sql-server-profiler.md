---
title: 暂停跟踪 （SQL Server 事件探查器） |Microsoft 文档
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
- pausing traces
- temporarily stopping traces
- traces [SQL Server], pausing
- stopping traces
ms.assetid: 432b9b0c-b5e7-47f3-a71b-310fb3bf2445
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e31b59bf2a71054f03982278b45e7b9e373f48e3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017445"
---
# <a name="pause-a-trace-sql-server-profiler"></a>暂停跟踪 (SQL Server Profiler)
  暂停跟踪可防止捕获更多的事件数据，直到重新启动该跟踪。  
  
 暂停跟踪可以防止捕获事件数据，直到重新启动跟踪。 重新启动跟踪将恢复跟踪操作。 重新启动后以前捕获的数据不会丢失。 重新启动跟踪时，将从启动的那一点恢复数据捕获。 暂停跟踪时，可以更改名称、事件、列和筛选器。 但是不能更改要将跟踪数据发送到的目标和服务器连接。  
  
### <a name="to-pause-a-trace"></a>暂停跟踪  
  
1.  选择一个包含正在运行的跟踪的窗口。  
  
2.  在 **“文件”** 菜单上，单击 **“暂停跟踪”**。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 事件探查器](sql-server-profiler.md)  
  
  