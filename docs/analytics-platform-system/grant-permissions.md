---
title: 授予 T-SQL 的权限-并行数据仓库 |Microsoft Docs
description: 并行数据仓库中的数据库操作的 Grant T-SQL 的权限。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 01ef7b199a07be8bbc2dc1dee40d9c4d5771db1b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63157496"
---
# <a name="grant-t-sql-permissions-for-parallel-data-warehouse"></a>并行数据仓库的 Grant T-SQL 的权限
并行数据仓库中的数据库操作的 Grant T-SQL 的权限。

## <a name="grant-permissions-to-submit-database-queries"></a>授予权限来提交数据库查询
本部分介绍如何授予数据库角色权限的用户在 SQL Server PDW 设备上的查询数据。  
  
用于授予权限来查询数据的语句取决于所需的访问范围。 以下 SQL 语句创建一个登录名可以访问设备，请创建一个名为 KimAbercrombie 中的数据库用户的 KimAbercrombie **AdventureWorksPDW2012**数据库，创建名为 PDWQueryData 的数据库角色，添加使用是否在对象或数据库级别授予访问权限基于 KimAbercrombie 到 PDWQueryData 角色，然后对其授予查询访问的显示选项。  
  
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
  
## <a name="grant-permissions-to-use-the-admin-console"></a>授予权限以使用管理控制台
本部分介绍如何授予对登录名的权限，以使用管理控制台。  
  
**使用管理控制台**  
  
若要使用管理控制台登录名需要服务器级别**VIEW SERVER STATE**权限。 以下 SQL 语句授予**VIEW SERVER STATE**登录名具有权限`KimAbercrombie`以便 Kim 可以使用管理控制台以监视 SQL Server PDW 设备。  
  
```sql  
USE master;  
GO  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
GO  
```  
  
**终止会话**  
  
若要终止会话的权限授予登录名，授予**ALTER ANY CONNECTION**权限，如下所示：  
  
```sql  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
## <a name="grant-permissions-to-load-data"></a>授予权限来加载数据
本部分介绍如何授予数据加载到 SQL Server PDWappliance 数据库角色和数据库用户的权限。  
  
以下脚本显示了哪些权限所需的每个加载选项。 您可以修改此选项以满足特定需求。  
  
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
  
## <a name="grant-permissions-to-copy-data-off-the-appliance"></a>在设备以外授予的权限将数据复制
本部分介绍如何授予用户或数据库角色授予权限，才能复制 SQL Server PDW 设备中的数据。  
  
若要将数据移到另一个位置，需要**选择**权限，才能移动包含数据的表。  
  
如果数据的目标是另一个 SQL Server PDW，用户必须拥有**CREATE TABLE**目标位置的权限和**ALTER SCHEMA**将包含表的架构权限。  
  
## <a name="grant-permissions-to-manage-databases"></a>授予权限来管理数据库
本部分介绍如何向要管理 SQL Server PDW 设备上的数据库的数据库用户授予权限。  
  
在某些情况下，一家公司将分配数据库的管理器。 该管理器控制其他登录名具有对该数据库，以及数据和数据库中的对象的访问权限。 若要管理所有对象，角色，并在数据库中的用户授予用户**控制**针对数据库的权限。 下面的语句授予**控制**上的权限**AdventureWorksPDW2012**数据库添加到用户`KimAbercrombie`。  
  
```sql
USE AdventureWorksPDW2012;  
GO  
GRANT CONTROL ON DATABASE:: AdventureWorksPDW2012 TO KimAbercrombie;  
```  
  
若要授予用户权限来控制设备上的所有数据库，授予**ALTER ANY DATABASE** master 数据库中的权限。  
  
## <a name="grant-permissions-to-manage-logins-users-and-database-roles"></a>授予管理用户的登录名和数据库角色的权限
本部分介绍如何授予权限来管理登录名、 数据库用户和数据库角色。  
  
### <a name="PermsAdminConsole"></a>授予权限来管理登录名  
**添加或管理登录名**  
  
以下 SQL 语句创建一个登录名可以通过使用创建新的登录名的 KimAbercrombie [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)语句和使用更改现有登录名[ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)语句。  
  
**ALTER ANY LOGIN**权限授予创建新的登录名和删除现有的功能。 后一个登录名存在，可以通过有登录名管理登录名**ALTER ANY LOGIN**权限或**ALTER**该登录名的权限。 登录名可以更改用于自身登录的密码和默认数据库。  
  
```sql 
CREATE LOGIN KimAbercrombie   
WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
GRANT ALTER ANY LOGIN TO KimAbercrombie;  
```  
  
### <a name="grant-permissions-to-manage-login-sessions"></a>授予权限来管理登录会话  
若要能够在服务器上查看所有会话，需要**都 VIEW SERVER STATE**权限。 若要终止的其他登录名会话的功能需要**ALTER ANY CONNECTION**权限。 下面的示例使用`KimAbercrombie`前面创建的登录名。  
  
```sql  
-- Grant permissions to view sessions and queries  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
  
-- Grant permission to end sessions  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
### <a name="grant-permission-to-manage-database-users"></a>授予权限来管理数据库用户  
创建和删除数据库用户需要**ALTER ANY USER**权限。 管理现有用户需要**ALTER ANY USER**权限或**ALTER**对该用户的权限。 下面的示例使用`KimAbercrombie`前面创建的登录名。  
  
```sql  
-- Create a user  
USE AdventureWorksPDW2012;  
GO  
CREATE USER KimAbercrombie;  
  
-- Grant permissions to create and drop users   
GRANT ALTER ANY USER TO KimAbercrombie;  
```  
  
### <a name="grant-permisson-to-manage-database-roles"></a>授予权限来管理数据库角色  
创建和删除用户定义的数据库角色需要**ALTER ANY ROLE**权限。 下面的示例使用`KimAbercrombie`登录名和前面创建的使用。  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
-- Grant permissions to create and drop roles  
GRANT ALTER ANY ROLE TO KimAbercrombie;  
```  
  
### <a name="login-user-and-role-permission-charts"></a>登录名、 用户和角色权限图表  
下面的图表可能会造成混淆，但它们显示 （如控件） 的方式更高级别权限包括更加细化可以单独 （如 ALTER) 授予的权限。 它是始终授予权限的人来完成其必要任务量最少的最佳做法。 若要执行此操作，授予更具体的权限，而不是最高级别权限。  
  
**登录名的权限：**  
  
![APS 安全性登录权限](./media/grant-permissions/APS_security_login_perms.png "APS_security_login_perms")  
  
**用户权限：**  
  
![APS 安全性用户权限](./media/grant-permissions/APS_security_user_perms.png "APS_security_user_perms")  
  
**角色权限：**  
  
![APS 安全性角色权限](./media/grant-permissions/APS_security_role_perms.png "APS_security_role_perms")  
  
<!-- MISSING LINKS
For a list of all permissions, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  
  
-->

## <a name="grant-permissions-to-monitor-the-appliance"></a>授予用于监视设备的权限
可以通过使用管理控制台或 SQL Server PDW 系统视图监视 SQL Server PDW 设备。 登录名需要服务器级别**VIEW SERVER STATE**监视设备的权限。 登录名需要**ALTER ANY CONNECTION**通过使用管理控制台终止连接的权限或**终止**命令。 若要使用管理控制台所需的权限的信息，请参阅[授予权限以使用管理控制台&#40;SQL Server PDW&#41;](#grant-permissions-to-use-the-admin-console)。  
  
### <a name="PermsAdminConsole"></a>授予权限以使用系统视图监视设备  
以下 SQL 语句创建一个登录名`monitor_login`，并授予**VIEW SERVER STATE**权`monitor_login`登录名。  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_login WITH PASSWORD='Password4321';  
GRANT VIEW SERVER STATE TO monitor_login;  
GO  
```  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views-and-to-terminate-connections"></a>授予的权限以使用系统视图监视设备，并终止连接  
以下 SQL 语句创建一个登录名`monitor_and_terminate_login`，并授予**VIEW SERVER STATE**并**ALTER ANY CONNECTION**权`monitor_and_terminate_login`登录名。  
  
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
[CREATE USER](../t-sql/statements/create-user-transact-sql.md)  
[CREATE ROLE](../t-sql/statements/create-role-transact-sql.md)  
[加载](load-overview.md)  
