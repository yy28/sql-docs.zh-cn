---
title: "工作负荷管理任务"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/12/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.openlocfilehash: eeeaded31dcbb67dfcd6f7ff1a99745ca27e9e7e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="workload-management-tasks"></a>工作负荷管理任务

## <a name="view-login-members-of-each-resource-class"></a>查看登录名的每个资源类的新成员
描述如何在 SQL Server PDW 中显示每个资源类服务器角色的登录名成员。 使用此查询以了解允许的提交的每个登录名的请求的资源的类。  
  
资源类描述，请参阅[工作负荷管理](workload-management.md)。  
  
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
  
如果登录名不是此列表中，其请求将收到的默认资源。 如果登录名是多个资源类的成员，最大类具有优先级。  
  
中列出的资源分配[工作负荷管理](workload-management.md)主题。  
  
## <a name="change-the-system-resources-allocated-to-a-request"></a>更改分配给请求的系统资源
描述如何找出哪些资源的 SQL Server PDW 请求运行时所使用的类以及如何更改该请求的系统资源。 更改资源请求需要更改已提交请求时，使用的登录名的资源类成员身份，以便[ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md)语句。  
  
### <a name="step-1-determine-the-resource-class-for-the-login-running-the-request"></a>步骤 1： 确定运行请求的登录名的资源类。  
此查询显示哪些是资源类服务器角色成员身份的成员的登录名。 有三个资源类， **mediumrc**， **largerc**，和**xlargerc**。  
  
> [!IMPORTANT]  
> 必须通过登录名具有执行此查询**CONTROL SERVER**权限。 如果执行者没有登录**CONTROL SERVER**权限，此查询仅返回当前的登录名的角色成员身份。  
  
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
  
如果没有资源类服务器角色的成员的登录名，则生成的表将为空。 在这种情况下，如果查询返回一个登录名 Ching，然后在 Ching 提交请求，请求将收到的默认系统资源，该值小于资源类系统资源。 如果登录名是多个资源类的成员，最大类具有优先级。  
  
对于每个资源类的资源分配的列表，请参阅[工作负荷管理](workload-management.md)主题。  
  
### <a name="step-2-run-the-request-under-a-login-with-different-resource-class-membership"></a>步骤 2： 使用不同的资源类成员资格运行下一个登录名的请求  
有两种方法，以运行与任一放大或缩小系统资源的请求：  
  
-   运行在不同的登录请求是一个更大或更小的资源类的成员。  
  
-   将必要的登录名添加到资源类角色之一。 选择此选项时要格外小心;更改该登录名的资源类将更改提交的登录名的所有请求的系统资源级别。  
  
假定 Ching largerc 服务器角色的成员。 下面的示例演示如何将登录 Ching 添加到 xlargerc 服务器角色。  
  
```sql  
ALTER SERVER ROLE xlargerc ADD MEMBER Ching;  
```  
  
Ching 现 largerc 和 xlargerc 服务器角色的成员。 当 Ching 提交请求时，请求将收到 xlargerc 系统资源。  
  
下面的示例移 Ching 回 mediumrc 服务器角色。  为此，她必须从被删除 xlargerc 和 largerc 服务器角色，并添加到 mediumrc 服务器角色。  
  
```sql  
-- Move login Ching back to using medium system resources for requests.  
ALTER SERVER ROLE xlargerc DROP MEMBER Ching;  
ALTER SERVER ROLE largerc DROP MEMBER Ching;  
ALTER SERVER ROLE mediumrc ADD MEMBER Ching;  
```  
  
Ching 现 mediumrc 服务器角色的成员。  以下示例更改 Ching 能够她请求的默认系统资源。  
  
```sql  
-- Move login Ching to use the default system resources for requests.  
ALTER SERVER ROLE mediumrc DROP MEMBER Ching;  
```  
  
有关更改资源类角色成员身份的详细信息，请参阅[ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md)。  

## <a name="change-a-login-to-the-default-system-resources-for-its-requests"></a>将登录名更改为其请求的默认系统资源
介绍如何更改分配给 SQL Server PDW 登录名添加到默认金额的系统资源分配。 这会影响 SQL Server PDW 将分配给请求提交的登录名的系统资源。  
  
资源类描述，请参阅[工作负荷管理](workload-management.md)  
  
如果登录名不是任何资源类服务器角色的成员，提交的登录名的请求可获得默认的系统资源量。  
  
假设 Matt 是当前的所有资源类服务器角色的成员，并且想要还原为其接收只有的默认资源的请求的登录名。  下面的示例通过删除所有三个资源类服务器角色的成员身份将默认资源分配给 Matt 的请求。  
  
```sql  
--Give the requests submitted by Matt the default system resources   
--by dropping Matt from all resource class server roles.  
ALTER SERVER ROLE XLargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE LargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE MediumRC DROP MEMBER Matt;  
```  
  
## <a name="display-the-number-of-concurrency-slots-needed-for-a-waiting-request"></a>显示请求的数量的并发槽需要等待
描述如何推断出的并发槽所需的正在等待在 SQL Server PDW 上运行的请求数。  
  
有关详细信息，请参阅[工作负荷管理](workload-management.md)。  
  
请求无法等待很长时间没有正在执行。 若要解决此问题的方法之一是查看请求需要的并发槽的数目。  下面的示例显示所需的每个正在等待的请求的并发槽数。  
  
```sql  
--Display the number of concurrency slots required   
--for each request that is waiting to run.  
SELECT request_id, concurrency_slots_used AS [Slots Needed], resource_class AS [Resource Class]  
FROM sys.dm_pdw_resource_waits;  
```  
  
  
## <a name="see-also"></a>另请参阅  
[工作负荷管理](workload-management.md)  
  
