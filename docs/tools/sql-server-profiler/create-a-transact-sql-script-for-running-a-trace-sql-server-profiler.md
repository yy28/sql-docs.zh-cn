---
title: 创建 Transact-SQL 脚本来运行跟踪 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], running
- scripts [SQL Server], traces
ms.assetid: 6b0e2519-998d-40d5-b8ba-5e6a773f91a6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 88e21aa7d02dfbf1a54f11e800e165f7055d2892
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62712509"
---
# <a name="create-a-transact-sql-script-for-running-a-trace-sql-server-profiler"></a>创建 Transact-SQL 脚本来运行跟踪 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题说明了如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]从现有的跟踪文件或表中创建 Transact-SQL 脚本。  
  
### <a name="to-create-a-transact-sql-script-to-run-a-trace"></a>创建 Transact-SQL 脚本来运行跟踪  
  
1.  打开跟踪文件或表。 有关详细信息，请参阅 [打开跟踪文件 (SQL Server Profiler)](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) 或 [打开跟踪表 (SQL Server Profiler)](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)一起提供的预定义优化模板。  
  
2.  在“文件”  菜单上，依次指向“导出”  和“脚本跟踪定义”  ，然后单击与你要跟踪的服务器对应的版本。  
  
3.  在 **“另存为”** 对话框中，输入脚本文件名称，然后单击 **“保存”** 。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Profiler 模板和权限](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server 事件探查器](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
