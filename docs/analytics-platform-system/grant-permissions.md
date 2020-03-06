---
title: 授予 T-sql 权限
description: 为并行数据仓库中的数据库操作授予 T-sql 权限。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6bbe78979c393490a52e1051fe158ae138f93dcc
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2020
ms.locfileid: "78339564"
---
# <a name="grant-t-sql-permissions-for-parallel-data-warehouse"></a>为并行数据仓库授予 T-sql 权限
为并行数据仓库中的数据库操作授予 T-sql 权限。

## <a name="grant-permissions-to-submit-database-queries"></a>授予提交数据库查询的权限
本部分介绍如何向数据库角色和用户授予对 SQL Server PDW 设备上的数据进行查询的权限。  
  
用于向查询数据授予权限的语句取决于所需的访问范围。 以下 SQL 语句创建名为 KimAbercrombie 的登录名，该登录名可访问该设备，在**AdventureWorksPDW2012**数据库中创建名为 KimAbercrombie 的数据库用户，创建名为 PDWQueryData 的数据库角色，将 use KimAbercrombie 添加到 PDWQueryData 角色，然后根据访问权限是在对象上还是在数据库级别显示来授予查询访问权限的选项。  
  
```sql  
USE master;  
GO  
  
CREATE LOGIN KimAbercrombie WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
USE AdventureWorksPDW2012;  
GO  
  
CREATE USER KimAbercrombie;  
GO  
  
CREATE ROLE PDWQueryData;  
GO  
  
EXEC sp_addrolemember 'PDWQueryData', 'KimAbercrombie'  
GO  
  
-- If the permission is granted against a table or view only, use this syntax:  
GRANT SELECT ON OBJECT::AdventureWorksPDW2012..DimEmployee TO PDWQueryData;  
GO  
  
-- If the permission is granted for the database, use this syntax:  
GRANT SELECT ON DATABASE::AdventureWorksPDW2012 TO PDWQueryData;  
GO  
  
-- If KimAbercrombie is the only user that needs to access a table, use this syntax:  
GRANT SELECT ON OBJECT::AdventureWorksPDW2012..DimEmployee TO KimAbercrombie;  
GO  
```  
  
## <a name="grant-permissions-to-use-the-admin-console"></a>授予使用管理控制台的权限
本部分介绍如何向登录名授予使用管理控制台的权限。  
  
**使用管理控制台**  
  
若要使用管理控制台，登录名需要服务器级别**VIEW SERVER STATE**权限。 下面的 SQL 语句向登录名`KimAbercrombie`授予**VIEW SERVER STATE**权限，以便 Kim 可以使用管理控制台监视 SQL Server PDW 设备。  
  
```sql  
USE master;  
GO  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
GO  
```  
  
**终止会话**  
  
若要向登录名授予终止会话的权限，请授予**ALTER ANY CONNECTION**权限，如下所示：  
  
```sql  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
## <a name="grant-permissions-to-load-data"></a>授予加载数据的权限
本部分介绍如何向数据库角色和数据库用户授予权限，以便将数据加载到 SQL Server PDWappliance 上。  
  
以下脚本显示每个加载选项所需的权限。 你可以对此进行修改以满足你的特定需求。  
  
```sql  
-- Create server login for the examples that follow.  
USE master;  
CREATE LOGIN BI_ETLUser WITH PASSWORD = '******';  
  
--Grant BULK Load permissions   
GRANT ADMINISTER BULK OPERATIONS TO BI_ETLUser;  
  
--Grant Staging database permissions  
USE stagedb;  
CREATE USER BI_ETLUser for login BI_ETLUser;  
EXEC sp_addrolemember 'db_datareader','BI_ETLUser';  
EXEC sp_addrolemember 'db_datawriter','BI_ETLUser';  
EXEC sp_addrolemember 'db_ddladmin','BI_ETLUser';  
  
-- The CREATE TABLE permission is required for the database hosting the temporary table.  
-- This may be the staging database (if specified) or destination database.   
-- The CREATE permission is not required if loading in fastappend mode.  
GRANT CREATE TABLE ON database::stagedb TO BI_ETLUser;  
  
-- If loading in append or fastappend mode, the INSERT permission is required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
  
-- If loading in reload mode, the INSERT and DELETE permissions are required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
GRANT DELETE ON database::stagedb TO BI_ETLUser;  
  
-- If loading in upsert mode, the INSERT and UPDATE permissions are required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
GRANT UPDATE ON database::stagedb TO BI_ETLUser;  
  
-- Destination DB  
USE tpch_1gb;  
CREATE USER BI_ETLUser FOR LOGIN BI_ETLUser;  
EXEC sp_addrolemember 'db_datareader','BI_ETLUser';  
EXEC sp_addrolemember 'db_datawriter','BI_ETLUser';  
```  
  
## <a name="grant-permissions-to-copy-data-off-the-appliance"></a>授予复制数据关闭设备的权限
本部分介绍如何向用户或数据库角色授予权限，以便将数据从 SQL Server PDW 设备中复制。  
  
若要将数据移到另一个位置，需要对包含要移动的数据的表具有**SELECT**权限。  
  
如果数据的目标是另一个 SQL Server PDW，则用户必须在目标上具有**CREATE TABLE**权限，并且对将包含该表的架构具有**ALTER schema**权限。  
  
## <a name="grant-permissions-to-manage-databases"></a>授予管理数据库的权限
本部分介绍如何向数据库用户授予管理 SQL Server PDW 设备上数据库的权限。  
  
在某些情况下，公司为数据库分配了经理。 管理器控制其他登录名对数据库的访问权限，以及数据库中的数据和对象。 若要管理数据库中的所有对象、角色和用户，请向用户授予对数据库的**CONTROL**权限。 下面的语句向用户`KimAbercrombie`授予对**AdventureWorksPDW2012**数据库的**CONTROL**权限。  
  
```sql
USE AdventureWorksPDW2012;  
GO  
GRANT CONTROL ON DATABASE:: AdventureWorksPDW2012 TO KimAbercrombie;  
```  
  
若要授予某个用户控制设备上所有数据库的权限，请在 master 数据库中授予**ALTER ANY DATABASE**权限。  
  
## <a name="grant-permissions-to-manage-logins-users-and-database-roles"></a>授予管理登录名、用户和数据库角色的权限
本部分介绍如何授予管理登录名、数据库用户和数据库角色的权限。  
  
### <a name="PermsAdminConsole"></a>授予管理登录名的权限  
**添加或管理登录名**  
  
以下 SQL 语句创建名为 KimAbercrombie 的登录名，该登录名可使用[CREATE login](../t-sql/statements/create-login-transact-sql.md)语句创建新的登录名，并使用[alter login](../t-sql/statements/alter-login-transact-sql.md)语句更改现有登录名。  
  
**ALTER ANY LOGIN**权限授予创建新登录名和删除现有登录名的功能。 登录名存在后，可以使用**ALTER ANY login**权限或对该登录名具有**alter**权限的登录名来管理该登录名。 登录名可以为自己的登录名更改密码和默认数据库。  
  
```sql 
CREATE LOGIN KimAbercrombie   
WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
GRANT ALTER ANY LOGIN TO KimAbercrombie;  
```  
  
### <a name="grant-permissions-to-manage-login-sessions"></a>授予管理登录会话的权限  
若要能够查看服务器上的所有会话，需要具有**VIEW SERVER STATE**权限。 若要终止其他登录会话，需要具有**ALTER ANY CONNECTION**权限。 下面的示例使用前面`KimAbercrombie`创建的登录名。  
  
```sql  
-- Grant permissions to view sessions and queries  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
  
-- Grant permission to end sessions  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
### <a name="grant-permission-to-manage-database-users"></a>授予管理数据库用户的权限  
创建和删除数据库用户需要**ALTER ANY USER**权限。 管理现有用户需要对该用户具有**ALTER ANY USER**权限或**alter**权限。 下面的示例使用前面`KimAbercrombie`创建的登录名。  
  
```sql  
-- Create a user  
USE AdventureWorksPDW2012;  
GO  
CREATE USER KimAbercrombie;  
  
-- Grant permissions to create and drop users   
GRANT ALTER ANY USER TO KimAbercrombie;  
```  
  
### <a name="grant-permisson-to-manage-database-roles"></a>授予权限管理数据库角色的权限  
创建和删除用户定义的数据库角色需要**ALTER ANY ROLE**权限。 下面的示例使用前面`KimAbercrombie`创建的登录名和使用。  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
-- Grant permissions to create and drop roles  
GRANT ALTER ANY ROLE TO KimAbercrombie;  
```  
  
### <a name="login-user-and-role-permission-charts"></a>登录名、用户和角色权限图表  
以下图表可能会令人感到困惑，但会显示更高的杠杆权限（如控制）如何包含可单独授予的更精细的权限（如 ALTER）。 最佳做法是始终授予人员完成其必要任务所需的最少权限。 为此，请授予更具体的权限，而不是顶级权限。  
  
**登录权限：**  
  
![APS 安全性登录权限](./media/grant-permissions/APS_security_login_perms.png "APS_security_login_perms")  
  
**用户权限：**  
  
![APS 安全性用户权限](./media/grant-permissions/APS_security_user_perms.png "APS_security_user_perms")  
  
**角色权限：**  
  
![APS 安全性角色权限](./media/grant-permissions/APS_security_role_perms.png "APS_security_role_perms")  
  
<!-- MISSING LINKS
For a list of all permissions, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  
  
-->

## <a name="grant-permissions-to-monitor-the-appliance"></a>授予监视设备的权限
SQL Server PDW 设备可以通过使用管理控制台或 SQL Server PDW 系统视图进行监视。 登录名需要服务器级别**VIEW SERVER STATE**权限来监视设备。 登录名需要**ALTER ANY CONNECTION**权限才能通过使用管理控制台或**KILL**命令终止连接。 有关使用管理控制台所需权限的信息，请参阅[授予使用管理员控制台 &#40;SQL Server PDW&#41;的权限](#grant-permissions-to-use-the-admin-console)。  
  
### <a name="PermsAdminConsole"></a>使用系统视图授予监视设备的权限  
以下 SQL 语句创建名为`monitor_login`的登录名，并向该`monitor_login`登录名授予**VIEW SERVER STATE**权限。  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_login WITH PASSWORD='Password4321';  
GRANT VIEW SERVER STATE TO monitor_login;  
GO  
```  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views-and-to-terminate-connections"></a>通过使用系统视图和终止连接来授予监视设备的权限  
`monitor_and_terminate_login`以下 SQL 语句创建名为的登录名，并授予该登录名的 "**查看服务器状态**" 和 "**更改任何连接**" `monitor_and_terminate_login`权限。  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_and_terminate_login WITH PASSWORD='Password1234';   
GRANT VIEW SERVER STATE TO monitor_and_terminate_login;   
GRANT ALTER ANY CONNECTION TO monitor_and_terminate_login;  
GO  
```  
  
若要创建管理员登录名，请参阅[固定服务器角色](pdw-permissions.md#fixed-server-roles)。  
  
## <a name="see-also"></a>另请参阅
[CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)  
[创建用户](../t-sql/statements/create-user-transact-sql.md)  
[CREATE ROLE](../t-sql/statements/create-role-transact-sql.md)  
[加载](load-overview.md)  
