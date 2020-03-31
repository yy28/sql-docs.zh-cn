---
title: 授予 T-SQL 权限
description: 为并行数据仓库中的数据库操作授予 T-SQL 权限。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6bbe78979c393490a52e1051fe158ae138f93dcc
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79289695"
---
# <a name="grant-t-sql-permissions-for-parallel-data-warehouse"></a>为并行数据仓库授予 T-SQL 权限
为并行数据仓库中的数据库操作授予 T-SQL 权限。

## <a name="grant-permissions-to-submit-database-queries"></a>授予提交数据库查询的权限
本节介绍如何授予数据库角色和用户在 SQL Server PDW 设备上查询数据的权限。  
  
用于授予查询数据权限的语句取决于所需的访问范围。 以下 SQL 语句创建名为 KimAbercrombie 的登录名，该登录名可以访问设备，在**AdventureWorksPD2012**数据库中创建名为 KimAbercrombie 的数据库用户，创建名为 PDWQueryData 的数据库角色，将使用 KimAbercrombie 添加到 PDWQueryData 角色，然后根据在对象级别或数据库级别授予访问，显示授予查询访问权限的选项。  
  
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
本节介绍如何授予登录方使用管理控制台的权限。  
  
**使用管理控制台**  
  
要使用管理控制台，登录需要服务器级**视图服务器状态**权限。 以下 SQL 语句向登录授予`KimAbercrombie`**"查看服务器状态"** 权限，以便 Kim 可以使用管理控制台监视 SQL Server PDW 设备。  
  
```sql  
USE master;  
GO  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
GO  
```  
  
**终止会话**  
  
要授予登录终止会话的权限，请使用以下方式授予**ALTER 任何连接**权限：  
  
```sql  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
## <a name="grant-permissions-to-load-data"></a>授予加载数据的权限
本节介绍如何授予数据库角色和数据库用户将数据加载到 SQL Server PDWappliance 的权限。  
  
以下脚本显示每个加载选项需要哪些权限。 您可以修改此功能以满足您的特定需求。  
  
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
  
## <a name="grant-permissions-to-copy-data-off-the-appliance"></a>授予从设备复制数据的权限
本节介绍如何向用户或数据库角色授予从 SQL Server PDW 设备复制数据的权限。  
  
要将数据移动到其他位置，需要在包含要移动数据的表上的**SELECT**权限。  
  
如果数据的目标是另一个 SQL Server PDW，则用户必须在目标上具有 **"创建表**"权限，并在包含表的架构上具有**ALTER SCHEMA**权限。  
  
## <a name="grant-permissions-to-manage-databases"></a>授予管理数据库的权限
本节介绍如何向数据库用户授予在 SQL Server PDW 设备上管理数据库的权限。  
  
在某些情况下，公司为数据库分配经理。 管理器控制其他登录对数据库的访问，以及数据库中的数据和对象。 要管理数据库中的所有对象、角色和用户，授予用户数据库的**CONTROL**权限。 以下语句将**AdventureWorksPDW2012**数据库的**CONTROL**权限授予用户`KimAbercrombie`。  
  
```sql
USE AdventureWorksPDW2012;  
GO  
GRANT CONTROL ON DATABASE:: AdventureWorksPDW2012 TO KimAbercrombie;  
```  
  
要授予某人控制设备上所有数据库的权限，请授予主数据库中的**ALTER ANY DATABASE**权限。  
  
## <a name="grant-permissions-to-manage-logins-users-and-database-roles"></a>授予管理登录名、用户和数据库角色的权限
本节介绍如何授予管理登录名、数据库用户和数据库角色的权限。  
  
### <a name="grant-permissions-to-manage-logins"></a><a name="PermsAdminConsole"></a>授予管理登录的权限  
**添加或管理登录名**  
  
以下 SQL 语句创建名为 KimAbercrombie 的登录名，该登录名可以使用[CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)语句创建新的登录名，并使用 ALTER [LOGIN](../t-sql/statements/alter-login-transact-sql.md)语句更改现有登录名。  
  
**ALTER 任何登录**权限授予创建新登录和删除删除权限的权限。 登录一旦存在，登录后，可以通过**具有 ALTER 任何登录**权限或该登录的**ALTER**权限的登录进行管理。 登录可以更改密码和默认数据库以进行自己的登录。  
  
```sql 
CREATE LOGIN KimAbercrombie   
WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
GRANT ALTER ANY LOGIN TO KimAbercrombie;  
```  
  
### <a name="grant-permissions-to-manage-login-sessions"></a>授予管理登录会话的权限  
要能够查看服务器上的所有会话，需要**查看服务器状态**权限。 终止其他登录会话的能力需要**ALTER 任何连接**权限。 下面的示例使用前面创建的`KimAbercrombie`登录名。  
  
```sql  
-- Grant permissions to view sessions and queries  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
  
-- Grant permission to end sessions  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
### <a name="grant-permission-to-manage-database-users"></a>授予管理数据库用户的权限  
创建和删除数据库用户需要**ALTER 任何用户**权限。 管理现有用户需要**ALTER 任何用户**权限或**该**用户的 ALTER 权限。 下面的示例使用前面创建的`KimAbercrombie`登录名。  
  
```sql  
-- Create a user  
USE AdventureWorksPDW2012;  
GO  
CREATE USER KimAbercrombie;  
  
-- Grant permissions to create and drop users   
GRANT ALTER ANY USER TO KimAbercrombie;  
```  
  
### <a name="grant-permisson-to-manage-database-roles"></a>授予 Permisson 管理数据库角色  
创建和删除用户定义的数据库角色需要**ALTER 任何 ROLE 权限**。 下面的示例使用之前创建的`KimAbercrombie`登录和使用。  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
-- Grant permissions to create and drop roles  
GRANT ALTER ANY ROLE TO KimAbercrombie;  
```  
  
### <a name="login-user-and-role-permission-charts"></a>登录、用户和角色权限图表  
以下图表可能会令人困惑，但它们显示了较高的杠杆权限（如 CONTROL）如何包含可以单独授予的更精细的权限（如 ALTER）。 最佳做法是始终为某人授予完成其必要任务的权限最少。 为此，授予更具体的权限，而不是顶级权限。  
  
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
可以使用管理控制台或 SQL Server PDW 系统视图监视 SQL Server PDW 设备。 登录需要服务器级**VIEW SERVER 状态**权限才能监视设备。 登录需要**ALTER 任何连接**权限才能使用管理控制台或**KILL**命令终止连接。 有关使用管理控制台所需的权限的信息，请参阅[授予使用管理控制台的权限&#40;SQL Server PDW&#41;](#grant-permissions-to-use-the-admin-console)。  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views"></a><a name="PermsAdminConsole"></a>授予使用系统视图监视设备的权限  
以下 SQL 语句创建名为的`monitor_login`登录名，并将 **"查看服务器状态"** 权限授予`monitor_login`登录名。  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_login WITH PASSWORD='Password4321';  
GRANT VIEW SERVER STATE TO monitor_login;  
GO  
```  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views-and-to-terminate-connections"></a>授予使用系统视图监视设备的权限和终止连接的权限  
以下 SQL 语句创建名为的`monitor_and_terminate_login`登录名，并将 **"查看服务器状态**"和 **"更改任何连接"** 权限授予`monitor_and_terminate_login`登录名。  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_and_terminate_login WITH PASSWORD='Password1234';   
GRANT VIEW SERVER STATE TO monitor_and_terminate_login;   
GRANT ALTER ANY CONNECTION TO monitor_and_terminate_login;  
GO  
```  
  
要创建管理员登录名，请参阅[固定服务器角色](pdw-permissions.md#fixed-server-roles)。  
  
## <a name="see-also"></a>请参阅
[CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)  
[创建用户](../t-sql/statements/create-user-transact-sql.md)  
[创建角色](../t-sql/statements/create-role-transact-sql.md)  
[加载](load-overview.md)  
