---
title: "运行 SQL Server 事件探查器 |Microsoft 文档"
ms.custom: 
ms.date: 7/7/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
- Profiler [SQL Server Profiler], running
- SQL Server Profiler, running
- running SQL Server Profiler
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
caps.latest.revision: "25"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7b875fa70017ce162ca50aa7d6d0235627d2f5f8
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2018
---
# <a name="run-sql-server-profiler"></a>运行 SQL Server Profiler
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]你可以运行[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]几种不同方式，以支持收集跟踪输出中的各种方案。 你可以开始[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]从使用 Windows 10**启动**菜单上，从**工具**菜单中的[!INCLUDE[ssDE](../../includes/ssde-md.md)]优化顾问，并从多个位置[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
当你首次启动[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]和选择**新跟踪**从**文件**菜单中，应用程序将显示**连接到服务器**对话框中，可以在其中指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]要连接到实例。  
## <a name="to-start-sql-server-profiler-from-the-windows-10-start-menu"></a>从 Windows 10 开始菜单启动 SQL Server 事件探查器  
-  单击 Windows**启动**图标或按 Windows 键，并开始键入"SQL Server 事件探查器 17"。 当**SQL Server 事件探查器 17**磁贴出现，请单击该。   

## <a name="to-start-sql-server-profiler-in-database-engine-tuning-advisor"></a>在数据库引擎优化顾问中启动 SQL Server Profiler  
-  在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问的 **“工具”** 菜单上，单击 **SQL Server Profiler**。  

## <a name="to-start-sql-server-profiler-in-sql-server-management-studio"></a>若要在 SQL Server Management Studio 中启动 SQL Server 事件探查器  
 你可以开始[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]从多个位置[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 当[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]启动时，它加载连接上下文、 跟踪模板及其启动点的筛选上下文。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]启动每个 SQL Server 事件探查器会话处于自己的实例，，探查器将继续运行，如果你关闭[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
### <a name="to-start-sql-server-profiler-from-the-tools-menu"></a>从“工具”菜单启动 SQL Server Profiler  
-  在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**工具**菜单上，单击**SQL Server 事件探查器**。  

### <a name="to-start-sql-server-profiler-from-the-query-editor"></a>从查询编辑器启动 SQL Server Profiler  
- 在查询编辑器中右键单击，然后选择“在 SQL Server Profiler 中跟踪查询” 。  

  > [!NOTE]  
  >  该连接上下文为编辑器连接，跟踪模板为 TSQL_SPs，应用的筛选器为 SPID = query window SPID。  
    
### <a name="to-start-sql-server-profiler-from-activity-monitor"></a>从活动监视器启动 SQL Server Profiler  
- 在活动监视器中，单击**进程**窗格中，右键单击你想要配置文件，然后单击的进程**在 SQL Server Profiler 中跟踪进程**。  

    > [!NOTE]  
    >  选定某个进程后，打开活动监视器时连接上下文为对象资源管理器连接。 跟踪模板为基于服务器类型的默认模板，并且 SPID 等于所选进程的 SPID。  
    
## <a name="net-framework-security"></a>.NET Framework 安全性  
- 在 Windows 身份验证模式下，用户帐户运行[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]必须有权连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
- 若要使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]执行跟踪，用户还必须拥有 ALTER TRACE 权限。  

## <a name="next-steps"></a>后续步骤  
 [SQL Server 事件探查器概述](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [使用 SQL Server Management Studio](http://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)  
