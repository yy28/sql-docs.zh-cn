---
title: 重播至光标处 （SQL Server 事件探查器） |Microsoft 文档
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: profiler
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- replaying cursors
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 89eadc41-4424-4a1c-ba61-0b52c851cdb1
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ead2018ba30ca61703fe266ee3cbbe88129fa444
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="replay-to-a-cursor-sql-server-profiler"></a>重播至光标处 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题介绍了如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]重播到光标处即暂停的跟踪文件或表。 在光标处暂停跟踪可支持调试，因为您可以将长跟踪脚本的重播分成较短的段，以便逐步进行分析。  
  
### <a name="to-replay-to-the-cursor"></a>重播至光标处  
  
1.  打开要重播的跟踪文件或跟踪表。 有关详细信息，请参阅 [打开跟踪文件 (SQL Server Profiler)](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) 或 [打开跟踪表 (SQL Server Profiler)](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)一起提供的预定义优化模板。  
  
     请确保打开的跟踪文件或跟踪表包含重播所需的事件类。 有关详细信息，请参阅 [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)。  
  
2.  在跟踪窗口中，单击一个事件。  
  
3.  在 **“重播”** 菜单上，单击 **“运行至光标处”**，然后连接到要重播跟踪的服务器。  
  
4.  在 **“重播配置”** 对话框中，验证设置，再单击 **“确定”**。  
  
     重播将开始，并在第一次到达光标处时暂停。  
  
5.  按 F5 恢复跟踪。  
  
6.  重复步骤 5 到跟踪的末尾。  
  
## <a name="see-also"></a>另请参阅  
 [重播到断点 (SQL Server Profiler)](../../tools/sql-server-profiler/replay-to-a-breakpoint-sql-server-profiler.md)   
 [重播跟踪](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server 事件探查器](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
