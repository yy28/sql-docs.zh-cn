---
title: 重播 Transact-SQL 脚本 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- scripts [SQL Server], traces
- replaying traces
ms.assetid: 9c0eb222-e6e3-4bc1-a25f-a41e962d361b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 62ca5b9038a8c5cfd7590ed2754691266a691c5f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906087"
---
# <a name="replay-a-transact-sql-script-sql-server-profiler"></a>重播 Transact-SQL 脚本 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  当测试性能问题的可能解决方案时，请使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 重播 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本，然后比较更改前后的性能。  
  
### <a name="to-replay-a-transact-sql-script"></a>重播 Transact-SQL 脚本  
  
1.  在 **“文件”** 菜单上，指向 **“打开”** ，然后单击 **“脚本文件”** 。  
  
2.  选择要打开的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本文件。 确保 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本包含要重播的事件。 有关详细信息，请参阅 [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)。  
  
3.  在 **“重播”** 菜单上，单击 **“启动”** ，连接到要重播脚本的服务器。  
  
4.  在 **“重播配置”** 对话框中，验证设置，再单击 **“确定”** 。  
  
## <a name="see-also"></a>另请参阅  
 [重播跟踪](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server 事件探查器](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
