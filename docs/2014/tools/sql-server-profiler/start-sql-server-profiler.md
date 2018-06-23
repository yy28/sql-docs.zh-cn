---
title: 启动 SQL Server 事件探查器 |Microsoft 文档
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
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9a61a8a5db0df279a344cdedfcf519c232cc911b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016015"
---
# <a name="start-sql-server-profiler"></a>启动 SQL Server Profiler
  可以通过多种方法启动 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ，以支持在各种情况下收集跟踪输出。 启动 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的方法包括：从 **“开始”** 菜单启动、从 **优化顾问中的** “工具” [!INCLUDE[ssDE](../../includes/ssde-md.md)] 菜单启动以及从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的多个位置启动。  
  
 首次启动 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 并从 **“文件”** 菜单中选择 **“新建跟踪”** 时，此应用程序将显示 **“连接到服务器”** 对话框，在该对话框中可以指定要连接到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
### <a name="to-start-sql-server-profiler-from-the-start-menu"></a>从“开始”菜单启动 SQL Server Profiler  
  
1.  在 **“开始”** 菜单中，依次指向 **“所有程序”**、 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]、 **“性能工具”**，然后单击 **SQL Server Profiler**。  
  
### <a name="to-start-sql-server-profiler-in-database-engine-tuning-advisor"></a>在数据库引擎优化顾问中启动 SQL Server Profiler  
  
1.  在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问的 **“工具”** 菜单上，单击 **SQL Server Profiler**。  
  
## <a name="starting-sql-server-profiler-in-management-studio"></a>在 Management Studio 中启动 SQL Server Profiler  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 启动的每个事件探查器会话处于自己的实例中，在关闭 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的情况下仍继续运行。  
  
 可以从 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 中的多个位置启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，如以下过程中所示。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 在启动时将加载连接上下文、跟踪模板及其启动点的筛选上下文。  
  
#### <a name="to-start-sql-server-profiler-from-the-tools-menu"></a>从“工具”菜单启动 SQL Server Profiler  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的“工具”菜单中，单击“SQL Server Profiler”。  
  
#### <a name="to-start-sql-server-profiler-from-the-query-editor"></a>从查询编辑器启动 SQL Server Profiler  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的菜单栏上，单击 **“新建查询”**。  
  
2.  在查询编辑器中右键单击，然后选择“在 SQL Server Profiler 中跟踪查询” 。  
  
    > [!NOTE]  
    >  该连接上下文为编辑器连接，跟踪模板为 TSQL_SPs，应用的筛选器为 SPID = query window SPID。  
  
#### <a name="to-start-sql-server-profiler-from-activity-monitor"></a>从活动监视器启动 SQL Server Profiler  
  
1.  在对象资源管理器中，右键单击 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例，然后单击“活动监视器” 。  
  
2.  单击“进程”  窗格，右键单击要探查的进程，然后单击“在 SQL Server Profiler 中跟踪进程” 。  
  
    > [!NOTE]  
    >  选定某个进程后，打开活动监视器时连接上下文为对象资源管理器连接。 跟踪模板为基于服务器类型的默认模板，并且 SPID 等于所选进程的 SPID。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 在 Windows 身份验证模式下，运行 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的用户帐户必须拥有连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的权限。  
  
 若要使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]执行跟踪，用户还必须拥有 ALTER TRACE 权限。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 事件探查器](sql-server-profiler.md)   
 [使用 SQL Server Management Studio](../../database-engine/use-sql-server-management-studio.md)  
  
  