---
title: "创建 TRANSACT-SQL 脚本来运行跟踪 （SQL Server 事件探查器） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], running
- scripts [SQL Server], traces
ms.assetid: 6b0e2519-998d-40d5-b8ba-5e6a773f91a6
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dac4e6f11ed6bb9bf5c7de2cd2780553cfe972f2
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-transact-sql-script-for-running-a-trace-sql-server-profiler"></a>创建 Transact-SQL 脚本来运行跟踪 (SQL Server Profiler)
  本主题说明了如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 从现有的跟踪文件或表中创建 Transact-SQL 脚本。  
  
### <a name="to-create-a-transact-sql-script-to-run-a-trace"></a>创建 Transact-SQL 脚本来运行跟踪  
  
1.  打开跟踪文件或表。 有关详细信息，请参阅[打开跟踪文件 (SQL Server Profiler)](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) 或[打开跟踪表 (SQL Server Profiler)](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)。  
  
2.  在“文件”菜单上，依次指向“导出”和“脚本跟踪定义”，然后单击与你要跟踪的服务器对应的版本。  
  
3.  在 **“另存为”** 对话框中，输入脚本文件名称，然后单击 **“保存”**。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Profiler 模板和权限](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server 事件探查器](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
