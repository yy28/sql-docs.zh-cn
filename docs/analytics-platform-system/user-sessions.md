---
title: 用户会话 (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0425cef2-de4d-4f42-91c5-cb1cd4bb1265
caps.latest.revision: 15
ms.openlocfilehash: 4ed0fab1fae1fe2d1a5a3ebb961d6c4d4747764f
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="user-sessions"></a>用户会话
具有适当的权限的登录名可以管理 SQL Server PDW 设备，包括执行这些操作的所有登录名的会话：  
  
-   在设备，包括活动和空闲会话上查看当前会话。  
  
-   为会话中查看的活动和最新的查询。  
  
-   结束活动会话。  
  
可以通过使用执行这些操作[通过使用管理控制台监视设备](monitor-the-appliance-by-using-the-admin-console.md)或[系统视图](tsql-system-views.md)通过 SQL 命令，如下所示。  
  
通过使用任何一种方法管理会话所需的权限相同，和中所述[为管理登录名、 用户和数据库角色授予权限](grant-permissions.md#grant-permissions-to-manage-logins-users-and-database-roles)。  
  
## <a name="manage-sessions-by-using-the-admin-console"></a>通过使用管理控制台管理会话  
  
### <a name="to-view-current-sessions-by-using-the-admin-console"></a>若要通过使用管理控制台来查看当前会话  
  
1.  在顶部菜单中，单击**会话**。  
  
2.  生成的列表显示所有最近使用的会话。 若要查看仅有效或空闲的会话，请单击**状态**列标题以按状态排序结果。  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-the-admin-console"></a>可以通过使用管理控制台中查看会话的活动和最新的查询  
  
1.  在顶部菜单中，单击**会话**。  
  
2.  在结果列表中，单击所需的会话的会话 ID。  
  
3.  生成的查询列表显示为会话的最新的查询。 有关查看查询详细信息的信息，请参阅[监视活动查询](monitoring-active-queries.md)。  
  
### <a name="to-end-sessions-by-using-the-admin-console"></a>若要通过使用管理控制台结束会话  
  
1.  在顶部菜单中，单击**会话**。  
  
2.  查找要取消会话的会话 ID。  
  
3.  单击红色**X**要结束会话的会话 ID 的左侧。 只有具有活动或空闲状态的会话将有一个红色**X**; 仅可以终止这些会话。  
  
## <a name="manage-sessions-by-using-system-views-and-sql-commands"></a>通过使用系统视图和 SQL 命令管理会话  
  
### <a name="to-view-current-sessions-by-using-system-views"></a>若要通过使用系统视图查看当前会话  
使用[sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)生成当前会话的列表。  
  
此示例返回所有会话的状态为 'Active' 或空闲 session_id、 login_name 和状态。  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions WHERE status='Active' OR status='Idle';  
```  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-system-views"></a>若要通过使用系统视图查看适用于会话的活动和最新查询  
若要查看与会话关联的活动和最近完成查询，你可以使用[sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)和[sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)视图。 此查询返回所有活动或空闲会话，以及与每个会话 id。 关联任何活动或最近查询的列表  
  
```sql  
SELECT es.session_id, es.login_name, es.status AS sessionStatus,   
er.request_id, er.status AS requestStatus, er.command   
FROM sys.dm_pdw_exec_sessions es   
LEFT OUTER JOIN sys.dm_pdw_exec_requests er   
ON (es.session_id=er.session_id)   
WHERE (es.status='Active' OR es.status='Idle') AND   
(er.status!= 'Completed' AND er.status!= 'Failed' AND er.status!= 'Cancelled');  
```  
  
### <a name="to-end-sessions-by-using-sql-commands"></a>若要使用 SQL 命令结束会话  
使用[终止](../t-sql/language-elements/kill-transact-sql.md)命令以结束当前会话。 你将需要进程终止，可使用中获取的会话 ID [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)视图。  
  
在此示例中，选择 login_name、 session_id 和状态值来查找基于登录名的会话。  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions;  
```  
  
可以通过使用 KILL 命令结束会话活动或空闲状态。  
  
```sql  
KILL 'SID137';  
```  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
