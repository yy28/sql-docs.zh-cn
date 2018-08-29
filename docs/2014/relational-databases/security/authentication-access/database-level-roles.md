---
title: 数据库级别的角色 | Microsoft Docs
ms.custom: ''
ms.date: 09/22/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server 2014
f1_keywords:
- sql12.swb.roleproperties.database.f1
- sql12.swb.roleproperties.general.f1
- sql12.swb.roleproperties.object.f1
- SQL12.SWB.DBROLEPROPERTIES.GENERAL.F1
helpviewer_keywords:
- db_denydatareader role
- users [SQL Server], database roles
- database-level roles [SQL Server]
- db_denydatawriter role
- roles [SQL Server], database
- principals [SQL Server], database-level
- db_backupoperator role
- credentials [SQL Server], roles
- db_accessadmin role
- schemas [SQL Server], roles
- permissions [SQL Server], roles
- database roles [SQL Server], listed
- db_datareader role
- db_ddladmin role
- db_datawriter role
- db_securityadmin role
- db_owner role
- database roles [SQL Server]
- fixed database roles [SQL Server]
- authentication [SQL Server], roles
- groups [SQL Server], roles
ms.assetid: 7f3fa5f6-6b50-43bb-9047-1544ade55e39
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 814b585d1ac15af1b083a3191ca44c32fe29e15e
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43027680"
---
# <a name="database-level-roles"></a>数据库级别的角色
  为便于管理数据库中的权限， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供了若干“角色”  ，这些角色是用于对其他主体进行分组的安全主体。 它们类似于 ***Windows 操作系统中的*** 组 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 。 数据库级角色的权限作用域为数据库范围。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中有两种类型的数据库级角色：数据库中预定义的“固定数据库角色”  和您可以创建的“灵活数据库角色”  。  
  
 固定数据库角色是在数据库级别定义的，并且存在于每个数据库中。 **db_owner** 数据库角色的成员可以管理固定数据库角色成员身份。 msdb 数据库中还有一些特殊用途的固定数据库角色。  
  
 可以向数据库级角色中添加任何数据库帐户和其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 角色。 固定数据库角色的每个成员都可向同一个角色添加其他登录名。  
  
> [!IMPORTANT]  
>  请不要将灵活数据库角色添加为固定角色的成员。 这会导致意外的权限升级。  
  
 下表显示了固定数据库级角色及其能够执行的操作。 所有数据库中都有这些角色。  
  
|数据库级别的角色名称|Description|  
|-------------------------------|-----------------|  
|**db_owner**|**db_owner** 固定数据库角色的成员可以执行数据库的所有配置和维护活动，还可以删除数据库。|  
|**db_securityadmin**|**db_securityadmin** 固定数据库角色的成员可以修改角色成员身份和管理权限。 向此角色中添加主体可能会导致意外的权限升级。|  
|**db_accessadmin**|**db_accessadmin** 固定数据库角色的成员可以为 Windows 登录名、Windows 组和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名添加或删除数据库访问权限。|  
|**db_backupoperator**|**db_backupoperator** 固定数据库角色的成员可以备份数据库。|  
|**db_ddladmin**|**db_ddladmin** 固定数据库角色的成员可以在数据库中运行任何数据定义语言 (DDL) 命令。|  
|**db_datawriter**|**db_datawriter** 固定数据库角色的成员可以在所有用户表中添加、删除或更改数据。|  
|**db_datareader**|**db_datareader** 固定数据库角色的成员可以从所有用户表中读取所有数据。|  
|**db_denydatawriter**|**db_denydatawriter** 固定数据库角色的成员不能添加、修改或删除数据库内用户表中的任何数据。|  
|**db_denydatareader**|**db_denydatareader** 固定数据库角色的成员不能读取数据库内用户表中的任何数据。|  
  
## <a name="msdb-roles"></a>msdb 角色  
 msdb 数据库中包含下表显示的特殊用途的角色。  
  
|msdb 角色名称|Description|  
|--------------------|-----------------|  
|`db_ssisadmin`<br /><br /> **db_ssisoperator**<br /><br /> **db_ssisltduser**|这些数据库角色的成员可以管理和使用 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]。 从早期版本升级的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例可能包含使用 Data Transformation Services (DTS)（而不是 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]）命名的旧版本角色。 有关详细信息，请参阅 [Integration Services Roles（SSIS 服务）](../../../integration-services/security/integration-services-roles-ssis-service.md)。|  
|`dc_admin`<br /><br /> **dc_operator**<br /><br /> **dc_proxy**|这些数据库角色的成员可以管理和使用数据收集器。 有关详细信息，请参阅 [Data Collection](../../data-collection/data-collection.md)。|  
|**PolicyAdministratorRole**|**db_ PolicyAdministratorRole** 数据库角色的成员可以对基于策略的管理策略和条件执行所有配置和维护活动。 有关详细信息，请参阅 [使用基于策略的管理来管理服务器](../../policy-based-management/administer-servers-by-using-policy-based-management.md)。|  
|**ServerGroupAdministratorRole**<br /><br /> **ServerGroupReaderRole**|这些数据库角色的成员可以管理和使用注册的服务器组。|  
|**dbm_monitor**|在中创建`msdb`在数据库镜像监视器中注册的第一个数据库时。 在系统管理员为 **dbm_monitor** 角色分配用户之前，该角色没有任何成员。|  
  
> [!IMPORTANT]  
>  db_ssisadmin 角色和 dc_admin 角色的成员可以将其特权提升为 sysadmin。 因为这些角色可以修改 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包，而 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理的 sysadmin 安全上下文可以执行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 包，所以可以实现特权提升。 若要在运行维护计划、数据收集组和其他 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包时防止此权限提升，请将运行包的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理作业配置为使用具有有限权限的代理帐户，或只将 sysadmin 成员添加到 db_ssisadmin 和 dc_admin 角色。  
  
## <a name="working-with-database-level-roles"></a>使用数据库级角色  
 下表说明了用于数据库级角色的命令、视图和函数。  
  
|功能|类型|Description|  
|-------------|----------|-----------------|  
|[sp_helpdbfixedrole (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql)|元数据|返回固定数据库角色的列表。|  
|[sp_dbfixedrolepermission (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dbfixedrolepermission-transact-sql)|元数据|显示固定数据库角色的权限。|  
|[sp_helprole (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helprole-transact-sql)|元数据|返回当前数据库中有关角色的信息。|  
|[sp_helprolemember (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql)|元数据|返回有关当前数据库中某个角色的成员的信息。|  
|[sys.database_role_members (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-role-members-transact-sql)|元数据|为每个数据库角色的每个成员返回一行。|  
|[IS_MEMBER (Transact-SQL)](/sql/t-sql/functions/is-member-transact-sql)|元数据|指示当前用户是否为指定 Microsoft Windows 组或 Microsoft SQL Server 数据库角色的成员。|  
|[CREATE ROLE (Transact-SQL)](/sql/t-sql/statements/create-role-transact-sql)|Command|在当前数据库中创建新的数据库角色。|  
|[ALTER ROLE (Transact-SQL)](/sql/t-sql/statements/alter-role-transact-sql)|Command|更改数据库角色的名称。|  
|[DROP ROLE (Transact-SQL)](/sql/t-sql/statements/drop-role-transact-sql)|Command|从数据库中删除角色。|  
|[sp_addrole (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addrole-transact-sql)|Command|在当前数据库中创建新的数据库角色。|  
|[sp_droprole (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-droprole-transact-sql)|Command|从当前数据库中删除数据库角色。|  
|[sp_addrolemember (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)|Command|为当前数据库中的数据库角色添加数据库用户、数据库角色、Windows 登录名或 Windows 组。|  
|[sp_droprolemember (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql)|Command|从当前数据库的 SQL Server 角色中删除安全帐户。|  
  
## <a name="public-database-role"></a>public 数据库角色  
 每个数据库用户都属于 **public** 数据库角色。 如果未向某个用户授予或拒绝对安全对象的特定权限时，该用户将继承授予该对象的 **public** 角色的权限。  
  
## <a name="related-content"></a>相关内容  
 [安全性目录视图 (Transact-SQL)](/sql/relational-databases/system-catalog-views/security-catalog-views-transact-sql)  
  
 [安全存储过程 (Transact-SQL)](/sql/relational-databases/system-stored-procedures/security-stored-procedures-transact-sql)  
  
 [安全函数 (Transact-SQL)](/sql/t-sql/functions/security-functions-transact-sql)  
  
 [保护 SQL Server](../securing-sql-server.md)  
  
 [sp_helprotect (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helprotect-transact-sql)  
  
  
