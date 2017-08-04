---
title: "重播 TRANSACT-SQL 脚本 （SQL Server 事件探查器） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], replaying
- scripts [SQL Server], traces
- replaying traces
ms.assetid: 9c0eb222-e6e3-4bc1-a25f-a41e962d361b
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: eed8da389f0c2422b3aee7ec947e5f34958f190d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="replay-a-transact-sql-script-sql-server-profiler"></a>重播 Transact-SQL 脚本 (SQL Server Profiler)
  当测试性能问题的可能解决方案时，请使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 重播 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本，然后比较更改前后的性能。  
  
### <a name="to-replay-a-transact-sql-script"></a>重播 Transact-SQL 脚本  
  
1.  在 **“文件”** 菜单上，指向 **“打开”**，然后单击 **“脚本文件”**。  
  
2.  选择要打开的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本文件。 确保 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本包含要重播的事件。 有关详细信息，请参阅 [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)。  
  
3.  在 **“重播”** 菜单上，单击 **“启动”**，连接到要重播脚本的服务器。  
  
4.  在 **“重播配置”** 对话框中，验证设置，再单击 **“确定”**。  
  
## <a name="see-also"></a>另请参阅  
 [重播跟踪](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server 事件探查器](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
