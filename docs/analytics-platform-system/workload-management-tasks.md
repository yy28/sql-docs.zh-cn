---
title: 工作负荷管理任务的分析平台系统 |Microsoft Docs
description: 分析平台系统中的工作负荷管理任务。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 8e538b96c482a6a16fffcfdac197e62885426b52
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63243802"
---
# <a name="workload-management-tasks-in-analytics-platform-system"></a>分析平台系统中的工作负荷管理任务
分析平台系统中的工作负荷管理任务。

## <a name="view-login-members-of-each-resource-class"></a>查看登录名的每个资源类的新成员
介绍如何在 SQL Server PDW 中显示每个资源类服务器角色的登录名成员。 使用此查询来找出资源允许的提交的每个登录名请求的类。  
  
资源类说明，请参阅[工作负荷管理](workload-management.md)。  
  
此查询显示每个资源类的成员身份列表。 有三个资源类、 mediumrc、 largerc 和 xlargerc。  
  
```sql  
SELECT l.name AS [member], r.name AS [server role]  
FROM sys.server_role_members AS rm  
JOIN sys.server_principals AS l  
  ON l.principal_id = rm.member_principal_id  
JOIN  
  sys.server_principals AS r  
  ON r.principal_id = rm.role_principal_id  
WHERE  
  ( l.[type] = 'S' OR l.[type] = 'U' OR l.[type] = 'G' )  
  AND r.[type] = 'R'  
  AND r.[name] in ('mediumrc', 'largerc', 'xlargerc');  
```  
  
如果登录名不是此列表中，其请求将收到的默认资源。 如果登录名是多个资源类的成员，最大的类将具有优先权。  
  
中列出的资源分配[工作负荷管理](workload-management.md)。  
  
## <a name="change-the-system-resources-allocated-to-a-request"></a>更改分配给请求的系统资源
介绍如何找出哪些资源类下，运行 SQL Server PDW 请求以及如何更改该请求的系统资源。 更改资源请求需要更改正在使用中提交请求，该登录名的资源类成员身份，以便[ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md)语句。  
  
### <a name="step-1-determine-the-resource-class-for-the-login-running-the-request"></a>第 1 步：确定登录名运行请求的资源类。  
此查询显示成员的资源类服务器角色成员身份的登录名。 有三个资源类， **mediumrc**， **largerc**，并**xlargerc**。  
  
> [!IMPORTANT]  
> 必须通过登录名拥有执行此查询**CONTROL SERVER**权限。 如果执行的登录名，而无需**CONTROL SERVER**权限，此查询仅返回当前登录名的角色成员身份。  
  
```sql  
SELECT l.name AS [member], r.name AS [server role]  
FROM sys.server_role_members AS rm  
JOIN sys.server_principals AS l  
  ON l.principal_id = rm.member_principal_id  
JOIN  
  sys.server_principals AS r  
  ON r.principal_id = rm.role_principal_id  
WHERE  
  l.[type] = 'S'   
  AND r.[type] = 'R'  
  AND r.[name] in ('mediumrc', 'largerc', 'xlargerc');  
GO  
```  
  
如果没有登录名的资源类服务器角色的成员，生成的表将为空。 在这种情况下，如果查询返回名为 Ching 的登录名，然后当 Ching 提交请求，请求将收到的默认系统资源，小于资源类系统资源。 如果登录名是多个资源类的成员，最大的类将具有优先权。  
  
每个资源类的资源分配的列表，请参阅[工作负荷管理](workload-management.md)。  
  
### <a name="step-2-run-the-request-under-a-login-with-different-resource-class-membership"></a>第 2 步：使用不同的资源类的成员身份运行下一个登录名的请求  
有两种方法以运行与任一更大或较小的系统资源的请求：  
  
-   运行在不同的登录名，放大或缩小资源类的成员的请求。  
  
-   需要登录名添加到资源类角色之一。 选择此选项时要注意;更改登录名的资源类将更改提交的登录名的所有请求的系统资源级别。  
  
假设 Ching 是 largerc 服务器角色的成员。 下面的示例演示如何向 xlargerc 服务器角色添加登录名 Ching。  
  
```sql  
ALTER SERVER ROLE xlargerc ADD MEMBER Ching;  
```  
  
Ching 现 largerc 和 xlargerc 服务器角色的成员。 当 Ching 提交请求时，请求将收到 xlargerc 系统资源。  
  
下面的示例将移 Ching 回 mediumrc 服务器角色。  若要将更改为新角色，必须从 xlargerc 和 largerc 服务器角色中删除该登录名并将其添加到 mediumrc 服务器角色。  
  
```sql  
-- Move login Ching back to using medium system resources for requests.  
ALTER SERVER ROLE xlargerc DROP MEMBER Ching;  
ALTER SERVER ROLE largerc DROP MEMBER Ching;  
ALTER SERVER ROLE mediumrc ADD MEMBER Ching;  
```  
  
Ching 现在是 mediumrc 服务器角色的成员。  下面的示例更改 Ching 具有请求的默认系统资源。  
  
```sql  
-- Move login Ching to use the default system resources for requests.  
ALTER SERVER ROLE mediumrc DROP MEMBER Ching;  
```  
  
有关更改资源类角色成员身份的详细信息，请参阅[ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md)。  

## <a name="change-a-login-to-the-default-system-resources-for-its-requests"></a>将登录名更改为其请求的默认系统资源
介绍如何更改分配给默认数量的 SQL Server PDW 登录系统资源分配。 
  
资源类说明，请参阅[工作负荷管理](workload-management.md)  
  
登录名不是任何资源类服务器角色的成员，在提交该登录名的请求将收到系统资源的默认数量。  
  
假设 Matt 当前为所有资源类服务器角色的成员，想要恢复到具有接收仅默认资源的请求的登录名。  下面的示例通过从所有三个资源类服务器角色中删除其成员身份将默认资源分配给 Matt 的请求。  
  
```sql  
--Give the requests submitted by Matt the default system resources   
--by dropping Matt from all resource class server roles.  
ALTER SERVER ROLE XLargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE LargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE MediumRC DROP MEMBER Matt;  
```  
  
## <a name="display-the-number-of-concurrency-slots-needed-for-a-waiting-request"></a>显示的并发槽数所需等待的请求
介绍如何找出的并发槽所需的正在等待 SQL Server PDW 上运行的请求数。  
  
有关详细信息，请参阅[工作负荷管理](workload-management.md)。  
  
无法执行不太长时间等待请求。 若要解决请求问题的方法之一是查看请求需要的并发槽数。  下面的示例显示了所需的每个正在等待的请求的并发槽数。  
  
```sql  
--Display the number of concurrency slots required   
--for each request that is waiting to run.  
SELECT request_id, concurrency_slots_used AS [Slots Needed], resource_class AS [Resource Class]  
FROM sys.dm_pdw_resource_waits;  
```  
  
  
## <a name="see-also"></a>请参阅  
[工作负荷管理](workload-management.md)  
  
