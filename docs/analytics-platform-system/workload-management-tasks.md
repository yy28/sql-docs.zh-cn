---
title: 工作负荷管理任务
description: 分析平台系统中的工作负荷管理任务。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 88d95eb0a2e0805930cb5f01f5af05b8fc6b3f2e
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399417"
---
# <a name="workload-management-tasks-in-analytics-platform-system"></a>分析平台系统中的工作负荷管理任务
分析平台系统中的工作负荷管理任务。

## <a name="view-login-members-of-each-resource-class"></a>查看每个资源类的登录成员
描述如何在 SQL Server PDW 中显示每个资源类服务器角色的登录成员。 使用此查询来确定允许用于每个登录名提交的请求的资源类。  
  
有关资源类的说明，请参阅[工作负荷管理](workload-management.md)。  
  
此查询显示每个资源类的成员资格列表。 有三个资源类： mediumrc、largerc 和 xlargerc。  
  
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
  
如果登录名不在此列表中，则其请求将接收默认资源。 如果登录名是多个资源类的成员，则最大的类优先。  
  
资源分配列在 "[工作负荷管理](workload-management.md)" 中。  
  
## <a name="change-the-system-resources-allocated-to-a-request"></a>更改分配给请求的系统资源
描述如何确定 SQL Server PDW 请求在其下运行的资源类，以及如何更改该请求的系统资源。 更改请求的资源需要更改提交请求的登录名的资源类成员身份，方法是使用[ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md)语句。  
  
### <a name="step-1-determine-the-resource-class-for-the-login-running-the-request"></a>步骤1：确定运行请求的登录名的资源类。  
此查询显示是资源类服务器角色成员身份的成员的登录名。 有三个资源类： **mediumrc**、 **largerc**和**xlargerc**。  
  
> [!IMPORTANT]  
> 此查询必须由具有**CONTROL SERVER**权限的登录名执行。 如果由没有**CONTROL SERVER**权限的登录名执行，则此查询只返回当前登录名的角色成员身份。  
  
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
  
如果没有资源类服务器角色成员的登录名，则生成的表将为空。 在这种情况下，如果查询返回名为 Ching 的登录名，则当 Ching 提交请求时，请求将收到默认系统资源，这些资源小于资源类系统资源。 如果登录名是多个资源类的成员，则最大的类优先。  
  
有关每个资源类的资源分配列表，请参阅[工作负荷管理](workload-management.md)。  
  
### <a name="step-2-run-the-request-under-a-login-with-different-resource-class-membership"></a>步骤2：在具有不同资源类成员身份的登录下运行请求  
可以通过两种方法运行具有较大或较小系统资源的请求：  
  
-   在作为更大或更小资源类成员的另一个登录帐户下运行请求。  
  
-   将必需的登录名添加到其中一个资源类角色。 请谨慎选择此选项;更改登录名的资源类将更改该登录名提交的所有请求的系统资源级别。  
  
假设 Ching 是 largerc 服务器角色的成员。 下面的示例演示如何将登录 Ching 添加到 xlargerc 服务器角色。  
  
```sql  
ALTER SERVER ROLE xlargerc ADD MEMBER Ching;  
```  
  
Ching 现在是 largerc 和 xlargerc 服务器角色的成员。 当 Ching 提交请求时，请求将收到 xlargerc 系统资源。  
  
下面的示例将 Ching 移回 mediumrc 服务器角色。  若要更改为新角色，必须从 xlargerc、largerc 服务器角色中删除登录名，并将其添加到 mediumrc 服务器角色。  
  
```sql  
-- Move login Ching back to using medium system resources for requests.  
ALTER SERVER ROLE xlargerc DROP MEMBER Ching;  
ALTER SERVER ROLE largerc DROP MEMBER Ching;  
ALTER SERVER ROLE mediumrc ADD MEMBER Ching;  
```  
  
Ching 现在是 mediumrc 服务器角色的成员。  下面的示例将 Ching 更改为具有请求的默认系统资源。  
  
```sql  
-- Move login Ching to use the default system resources for requests.  
ALTER SERVER ROLE mediumrc DROP MEMBER Ching;  
```  
  
有关更改资源类角色成员身份的详细信息，请参阅[ALTER SERVER role](../t-sql/statements/alter-server-role-transact-sql.md)。  

## <a name="change-a-login-to-the-default-system-resources-for-its-requests"></a>将登录名更改为其请求的默认系统资源
描述如何将分配给 SQL Server PDW 登录名的系统资源分配更改为默认数量。 
  
有关资源类的说明，请参阅[工作负荷管理](workload-management.md)  
  
如果登录名不是任何资源类服务器角色的成员，则该登录名提交的请求将接收默认数量的系统资源。  
  
假设登录名 Matt 当前是所有资源类服务器角色的成员，并且想要还原为请求仅接收默认资源。  下面的示例通过从所有三个资源类服务器角色中删除其成员身份，将默认资源分配给 Matt 的请求。  
  
```sql  
--Give the requests submitted by Matt the default system resources   
--by dropping Matt from all resource class server roles.  
ALTER SERVER ROLE XLargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE LargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE MediumRC DROP MEMBER Matt;  
```  
  
## <a name="display-the-number-of-concurrency-slots-needed-for-a-waiting-request"></a>显示等待请求所需的并发槽数
描述如何计算等待在 SQL Server PDW 上运行的请求所需的并发槽数。  
  
有关详细信息，请参阅[工作负荷管理](workload-management.md)。  
  
请求可能会等待很长时间，而不会执行。 解决请求的一种方法是查看请求所需的并发槽数。  下面的示例显示每个等待请求所需的并发槽数。  
  
```sql  
--Display the number of concurrency slots required   
--for each request that is waiting to run.  
SELECT request_id, concurrency_slots_used AS [Slots Needed], resource_class AS [Resource Class]  
FROM sys.dm_pdw_resource_waits;  
```  
  
  
## <a name="see-also"></a>另请参阅  
[工作负荷管理](workload-management.md)  
  
