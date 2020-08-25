---
title: 用户会话
description: 分析平台系统的并行数据仓库中的用户会话。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: a0e5b338cc616be214ef39527551ee4a6ffd8f56
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "74399398"
---
# <a name="user-sessions-in-analytics-platform-system"></a>分析平台系统中的用户会话
具有适当权限的登录名可以管理 SQL Server PDW 设备上所有登录的会话，包括执行以下操作：  
  
-   查看设备上的当前会话，包括活动和空闲会话。  
  
-   查看会话的活动查询和最近的查询。  
  
-   结束活动会话。  
  
通过使用管理控制台或[系统视图](tsql-system-views.md)通过 SQL 命令[监视设备](monitor-the-appliance-by-using-the-admin-console.md)，可以执行这些操作，如下所示。  
  
使用任一方法管理会话所需的权限都是相同的，在 [授予管理登录名、用户和数据库角色的权限](grant-permissions.md#grant-permissions-to-manage-logins-users-and-database-roles)中进行了介绍。  
  
## <a name="manage-sessions-by-using-the-admin-console"></a>使用管理控制台管理会话  
  
### <a name="to-view-current-sessions-by-using-the-admin-console"></a>使用管理控制台查看当前会话  
  
1.  在顶部菜单中，单击 " **会话**"。  
  
2.  生成的列表将显示最近的所有会话。 若要仅查看 "活动" 或 "空闲" 会话，请单击 " **状态** " 列标题以按状态对结果进行排序。  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-the-admin-console"></a>使用管理控制台查看会话的活动和最新查询  
  
1.  在顶部菜单中，单击 " **会话**"。  
  
2.  在结果列表中，单击所需会话的会话 ID。  
  
3.  生成的查询列表显示了针对该会话的最近查询。 有关查看查询详细信息的信息，请参阅 [监视活动查询](monitoring-active-queries.md)。  
  
### <a name="to-end-sessions-by-using-the-admin-console"></a>使用管理控制台结束会话  
  
1.  在顶部菜单中，单击 " **会话**"。  
  
2.  查找要取消的会话的会话 ID。  
  
3.  单击会话 ID 左侧的红色 **X** 以结束会话。 只有状态为 "活动" 或 "空闲" 的会话才会有红色 **X**;只有这些会话可以结束。  
  
## <a name="manage-sessions-by-using-system-views-and-sql-commands"></a>使用系统视图和 SQL 命令管理会话  
  
### <a name="to-view-current-sessions-by-using-system-views"></a>使用系统视图查看当前会话  
使用 [sys. dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) 生成当前会话的列表。  
  
此示例将返回状态为 "活动" 或 "空闲" 的所有会话的 session_id、login_name 和状态。  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions WHERE status='Active' OR status='Idle';  
```  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-system-views"></a>使用系统视图查看会话的活动和最新查询  
若要查看与会话关联的活动和最近完成的查询，请使用 [sys. dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) 和 [dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) 视图。 此查询返回所有活动或空闲会话的列表，以及与每个会话 ID 关联的所有活动或最近的查询。  
  
```sql  
SELECT es.session_id, es.login_name, es.status AS sessionStatus,   
er.request_id, er.status AS requestStatus, er.command   
FROM sys.dm_pdw_exec_sessions es   
LEFT OUTER JOIN sys.dm_pdw_exec_requests er   
ON (es.session_id=er.session_id)   
WHERE (es.status='Active' OR es.status='Idle') AND   
(er.status!= 'Completed' AND er.status!= 'Failed' AND er.status!= 'Cancelled');  
```  
  
### <a name="to-end-sessions-by-using-sql-commands"></a>使用 SQL 命令结束会话  
使用 [KILL](../t-sql/language-elements/kill-transact-sql.md) 命令结束当前会话。 你将需要终止进程的会话 ID，该 ID 可以使用 [sys. dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) 视图来获取。  
  
在此示例中，选择 "login_name"、"session_id" 和 "状态值"，基于登录名查找会话。  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions;  
```  
  
具有 "活动" 或 "空闲" 状态的会话可以使用 KILL 命令结束。  
  
```sql  
KILL 'SID137';  
```  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
