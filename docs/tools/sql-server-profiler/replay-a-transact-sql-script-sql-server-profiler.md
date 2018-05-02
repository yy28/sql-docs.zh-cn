---
title: 重播 Transact-SQL 脚本 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: sql-server-profiler
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], replaying
- scripts [SQL Server], traces
- replaying traces
ms.assetid: 9c0eb222-e6e3-4bc1-a25f-a41e962d361b
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 56c8590e3eacdc4f20fda834b5f2d8533ff61e68
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MTE
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="replay-a-transact-sql-script-sql-server-profiler"></a>重播 Transact-SQL 脚本 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  当测试性能问题的可能解决方案时，请使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 重播 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本，然后比较更改前后的性能。  
  
### <a name="to-replay-a-transact-sql-script"></a>重播 Transact-SQL 脚本  
  
1.  在 **“文件”** 菜单上，指向 **“打开”**，然后单击 **“脚本文件”**。  
  
2.  选择要打开的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本文件。 确保 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本包含要重播的事件。 有关详细信息，请参阅 [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)。  
  
3.  在 **“重播”** 菜单上，单击 **“启动”**，连接到要重播脚本的服务器。  
  
4.  在 **“重播配置”** 对话框中，验证设置，再单击 **“确定”**。  
  
## <a name="see-also"></a>另请参阅  
 [重播跟踪](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server 事件探查器](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
