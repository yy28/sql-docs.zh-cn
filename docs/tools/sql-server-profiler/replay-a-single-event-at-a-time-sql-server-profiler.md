---
title: 每次重播一个事件 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- events [SQL Server], replaying single event at a time
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 220fb192-9636-41a2-b15c-62af6cab8fff
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 91db80cd80b5e69bd9dee2c72c99eae6c76f166b
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67732950"
---
# <a name="replay-a-single-event-at-a-time-sql-server-profiler"></a>每次重播一个事件 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题介绍如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]每次重播跟踪文件或表中的一个事件。  
  
### <a name="to-replay-a-single-event-at-a-time"></a>每次重播一个事件  
  
1.  打开要重播的跟踪文件或跟踪表。 有关详细信息，请参阅 [打开跟踪文件 (SQL Server Profiler)](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) 或 [打开跟踪表 (SQL Server Profiler)](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)一起提供的预定义优化模板。  
  
     请确保打开的跟踪文件或跟踪表包含重播所需的事件类。 有关详细信息，请参阅 [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)。  
  
2.  在 **“重播”** 菜单上，单击 **“步骤”** ，然后连接到要在其上重播跟踪的服务器实例。  
  
3.  在 **“重播配置”** 对话框中，验证设置，再单击 **“确定”** 。 有关指定“重播配置”  对话框中的设置的详细信息，请参阅 [重播跟踪文件 (SQL Server Profiler)](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md) 或 [重播跟踪表 (SQL Server Profiler)](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)。  
  
4.  若要重播第一个事件，请单击 **“重播配置”** 对话框中的 **“确定”** 。  
  
5.  若要重播后续事件，请在 **“重播”** 菜单上，单击 **“步骤”** ，或按 F10。 对每个事件重复单击 **“步骤”** 或按 F10。  
  
## <a name="see-also"></a>另请参阅  
 [重播跟踪](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server 事件探查器](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
