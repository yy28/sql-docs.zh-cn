---
title: 并行数据仓库中的权限 |Microsoft Docs
description: 本文介绍的要求和用于管理并行数据仓库的数据库权限的选项。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1ac058e42b8bad4f499210835a1f85c3cc7a08a5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62639513"
---
# <a name="managing-permissions-in-parallel-data-warehouse"></a>并行数据仓库中的管理权限
本文介绍的要求和用于管理 SQL Server PDW 的数据库权限的选项。  
  
## <a name="BackupRestoreBasics"></a>数据库引擎权限基础知识  
SQL Server PDW 的数据库引擎权限由管理服务器级别通过登录名，并通过数据库用户和用户定义的数据库角色的数据库级别。  
  
**登录名**  
登录名是用于登录到 SQL Server PDW 的单个用户帐户。 SQL Server PDW 支持使用 Windows 身份验证和 SQL Server 身份验证的登录名。  Windows 身份验证登录名可以是 Windows 用户或 SQL Server PDW 信任任何域 Windows 组。 定义 SQL Server 身份验证登录名并将其通过 SQL Server PDW 的身份验证，并且必须创建通过指定密码。  
  
成员**sysadmin**固定的服务器角色 (如**sa**登录名) 而无需映射到数据库用户可以连接到数据库。 它们将映射到**dbo**用户。 数据库的所有者还映射为**dbo**用户。  
  
**服务器角色**  
有四个提供方便的服务器级别权限的组的预配置的角色的一组特殊的服务器角色。 **Sysadmin**， **MediumRC**， **LargeRC**，以及**XLargeRCfixed**服务器角色是当前在 SQL 中实现的唯一的服务器角色Server PDW。 **Sa**登录名是唯一的成员**sysadmin**固定的服务器角色和其他登录名不能添加到**sysadmin**角色。 可以授予登录名**CONTROL SERVER**权限，这是类似，但并不相同，到**sysadmin**固定的服务器角色。 使用[ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md)将成员添加到其他服务器角色。 SQL Server PDW 不支持用户定义的服务器角色。  
  
**数据库用户**  
登录名是通过在数据库中创建的数据库用户并将该数据库用户映射到登录名授予数据库访问权限。 通常，数据库用户名与登录名相同，尽管它不必要相同。 每个数据库用户均映射到单个登录名。 一个登录名只能映射到数据库中的一个用户，但可以映射为多个不同数据库中的数据库用户。  
  
**固定的数据库角色**  
固定的数据库角色是一组预配置提供方便组的数据库级权限的角色。 数据库用户和用户定义的数据库角色可以添加到使用固定的数据库角色[sp_addrolemember](../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)过程。 有关固定的数据库角色的详细信息，请参阅[固定数据库角色](#fixed-database-roles)。  
  
**用户定义的数据库角色**  
与用户**CREATE ROLE**权限可以创建新的用户定义数据库角色来表示具有公共权限的用户的组。 通常对整个角色授予或拒绝权限，从而简化了权限管理和监视。  
  
对安全主体 （登录名、 用户和角色） 授予权限，应使用**授予**语句。 通过使用显式拒绝权限**拒绝**命令。 使用删除以前授予或拒绝的权限**撤消**语句。 权限是累积的，用户将获得授予该用户、登录名和任何组成员身份的所有权限；但是任何权限拒绝将覆盖所有授予。 <!-- MISSING LINKS (For information, syntax, and available permissions with these commands, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md)).  -->  
  
下面的示例表示配置权限的常见和建议的方法。  
  
1.  如果使用 Windows 身份验证，创建每个 Windows 用户或将连接到 SQL Server PDW Windows 组登录的名。 如果使用 SQL Server 身份验证，请为每个人都将连接到 SQL Server PDW 创建登录名。  
  
2.  在所有必需的数据库中创建每个登录名的数据库用户。  
  
3.  创建一个或多个用户定义的数据库角色，每个资源表示一个类似的函数。 例如，财务分析人员和销售分析人员。  
  
4.  将数据库用户添加到一个或多个用户定义的数据库角色。  
  
5.  向用户定义的数据库角色授予权限。  
  
登录名是服务器级对象，可以通过查看列出[sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)。 只有服务器级权限可以授予服务器主体。  
  
用户和数据库角色是数据库级别对象，可以通过查看列出[sys.database_principals](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)。 仅对数据库主体可以授予数据库级别权限。  
  
## <a name="BackupTypes"></a>默认权限  
以下列表对默认权限进行了说明：  
  
-   Using 创建登录名时**CREATE LOGIN**语句中，登录名将接收**CONNECT SQL**权限允许登录名连接到 SQL Server PDW。  
  
-   通过使用创建数据库用户时**CREATE USER**语句中，用户会收到**CONNECT ON DATABASE::** _< 数据库名称 >_ 权限，允许要连接到该数据库作为用户登录名。  
  
-   由于隐式权限继承自的显式权限，包括公共角色的所有主体，默认情况下没有任何显式或隐式的权限。 因此，当存在时没有显式权限，可以也有任何隐式权限。  
  
-   当一个登录名变为对象或数据库的所有者时，该登录名始终具有对对象或数据库的所有权限。 不显示为显式权限所有权权限。 **GRANT**，**撤消**，并**拒绝**语句具有所有权权限没有影响。 可以使用更改所有权[ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md)语句。  
  
-   Sa 登录名在设备上具有所有权限。 类似于所有者权限，sa 权限无法更改，也不显示为显式权限。 **GRANT**，**撤消**，并**拒绝**语句具有 sa 权限没有影响。  
  
-   PUBLIC 服务器角色默认情况下接收任何权限，并不继承其他服务器角色的权限。 PUBLIC 服务器角色可授予显式权限与**GRANT**，**撤消**，并**拒绝**语句。  
  
-   事务不需要的权限。 可以运行的所有主体**BEGIN TRANSACTION**，**提交**，并**回滚**事务命令。 但是，主体必须具有适当的权限来运行每个语句在事务中。  
  
-   USE 语句不需要权限  。 可以运行的所有主体**使用**语句上任何数据库，但若要访问的数据库必须已用户主体数据库中，或者必须启用 guest 用户。  
  
### <a name="the-public-role"></a>公共角色  
所有新的设备登录名自动属于公共角色。 PUBLIC 服务器角色具有以下特征：  
  
-   PUBLIC 服务器角色默认情况下具有任何权限。  
  
-   所有主体都是 PUBLIC 服务器角色的成员和公共服务器角色不是另一个服务器角色的成员。  
  
-   PUBLIC 服务器角色不能继承隐式权限。 必须显式授予任何权限授予公共角色。  
  
## <a name="BackupProc"></a>确定权限  
登录名是否有权执行特定操作取决于对登录名、 用户和用户是其成员的角色授予或拒绝的权限。 服务器级权限 (如**CREATE LOGIN**并**VIEW SERVER STATE**) 可供服务器级主体 （登录名）。 数据库级权限 (如**选择**从表或**EXECUTE**对过程) 可供数据库级主体 （用户和数据库角色）。  
  
### <a name="implicit-and-explicit-permissions"></a>隐式和显式权限  
显式权限是 GRANT 或 DENY 语句给授予某主体的 GRANT 或 DENY 权限      。 中列出了数据库级别权限[sys.database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)视图。 中列出了服务器级权限[sys.server_permissions](../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)视图。  
  
*隐式权限*是**授予**或**拒绝**主体 （登录名或服务器角色） 已继承的权限。 可以按以下方式继承权限。  
  
-   主体可以继承权限角色如果主体是角色的成员，即使该主体不具有显式**GRANT**或**拒绝**权限。  
  
-   如果主体具有对一个对象父作用域 （如表或整个数据库的权限的架构） 的权限，主体可以继承一个从属对象 （如表） 的权限。  
  
-   主体可以通过让包括从属权限的权限继承权限。 例如**ALTER ANY USER**权限包括**CREATE USER**并**ALTER ON USER::** _<name>_ 权限。  
  
### <a name="determining-permissions-when-performing-actions"></a>执行操作时确定权限  
确定要分配给主体的权限复杂的过程。 确定隐式权限，因为主体可以是多个角色的成员和权限可通过角色层次结构中的多个级别时，会发生复杂性。  
  
以下列表描述用于确定权限的一般规则：  
  
-   所有权意味着权限。  
  
    对象所有者的对象上具有所有权限。 同样，数据库所有者拥有对数据库的所有权限和对象的所有权限的数据库中。 无法更改这些权限。  
  
-   可以跨多个服务器角色成员资格的层次结构中级别继承权限。  
  
    例如，假设有以下情况：  
  
    -   登录名 David 是数据库角色 PerfAnalysts 的成员。  
  
    -   PerfAnalysts 是生产的数据库角色的成员。  
  
    -   David 和 PerfAnalysts 没有**选择**客户表的权限。 权限已被吊销或永远不会显式授予。  
  
    -   生产已**选择**客户表的权限。  
  
    在这种情况下，将继承 PerfAnalysts**授予**从生产环境中，和 David 客户表的权限将继承**授予**从生产客户表的权限。  
  
-   **DENY**重写**授予**权限发生冲突时。  
  
    例如，假设登录名 David Customer 表中具有任何权限，并且是两个数据库角色的成员-dbgroup1，具有**拒绝**上的客户表和 dbgroup2，具有的权限**授予**Customer 表的权限。 在这种情况下，将继承 David**拒绝**客户表的权限。 无论角色获得其权限显式或隐式是这种情况。  
  
### <a name="auditing-permissions"></a>审核的权限  
若要检索的用户的权限检查以下各项。  
  
-   执行以下查询来确定哪些登录名是系统管理员。  
  
    ```sql  
    SELECT SPLogins.name, 'is a member of ', SPRoles.name   
    FROM sys.server_role_members AS SRM   
    JOIN sys.server_principals AS SPRoles   
        ON SRM.role_principal_id = SPRoles.principal_id   
    JOIN sys.server_principals AS SPLogins   
        ON SRM.member_principal_id = SPLogins.principal_id;  
    ```  
  
-   执行以下查询来确定哪些登录名已被授予显式权限。  
  
    ```sql  
    SELECT name, 'has the ', state_desc , permission_name, ' permission'  
    FROM sys.server_permissions AS SP  
    JOIN sys.server_principals AS SPRoles   
        ON SP.grantee_principal_id = SPRoles.principal_id;  
    ```  
  
-   若要确定哪些数据库用户是数据库角色的成员的用户数据库中执行以下查询。  
  
    ```sql  
    SELECT DPUsers.name, 'is a member of ', DPRoles.name    
    FROM sys.database_role_members AS DRM  
    JOIN sys.database_principals AS DPRoles   
        ON DRM.role_principal_id = DPRoles.principal_id  
    JOIN sys.database_principals AS DPUsers  
        ON DRM.member_principal_id = DPUsers.principal_id;  
    ```  
  
-   若要确定哪些数据库用户和角色被授予或拒绝特定权限的用户数据库中执行以下查询。 可以查询其他视图，例如 sys.objects 和 sys.schemas 标识与则 major_id 所述的项目。  
  
    ```sql  
    SELECT DPUsers.name, 'has the ', permission_name,   
    'permission on the item described as class = ', class, 'id = ', major_id  
    FROM sys.database_permissions AS DP  
    JOIN sys.database_principals AS DPUsers  
        ON DP.grantee_principal_id = DPUsers.principal_id;  
    ```  
  
## <a name="RestoreProc"></a>数据库权限最佳做法  
  
-   是实际的最精细级别授予的权限。 授予在表或视图级别的权限可能会变得难以管理。 但在数据库级别授予权限可能是过于宽松。 如果数据库与架构用于定义工作边界，也许对架构授予的权限是表级和数据库级别之间了相应的折衷。  
  
-   授予权限到角色，而不是用户或登录名。 通过使用角色而不用户管理权限轻松快速授予或撤消权限的用户或登录名的一组通过将它们移入或移出该角色。 当函数会切换到另一个用户时，权限可以保持不变在角色级别的角色成员身份更改时。  
  
-   向基于作业函数，并将根据公司组执行操作的作业函数角色的更高级别的组角色的角色授予权限。  
  
-   每个最终用户应具有唯一的登录名。 不允许用户共享的登录名。 为每个用户提供登录名可确保审核线索并简化权限管理。  
  
## <a name="fixed-database-roles"></a>固定数据库角色
SQL Server 提供了预配置的 （固定） 数据库级角色，以帮助你管理的服务器上的权限。 预配置的角色被固定的无法更改分配给他们的权限。 也可以创建用户定义的数据库角色。 可以更改分配给用户定义的数据库角色的权限。  
  
角色是可组合其他主体的安全主体。 数据库角色是数据库级权限作用域中。 为数据库角色的成员，可以添加数据库用户和其他数据库角色。 固定的数据库角色不能添加到每个其他。 （“角色”  类似于 Windows 操作系统中的“组”  。）  
  
有 9 固定的数据库角色。  
  
-   **db_owner**  
  
-   **db_securityadmin**  
  
-   **db_accessadmin**  
  
-   **db_backupoperator**  
  
-   **db_ddladmin**  
  
-   **db_datawriter**  
  
-   **db_datareader**  
  
-   **db_denydatawriter**  
  
-   **db_denydatareader**  
  
### <a name="permissions-of-the-fixed-database-roles"></a>固定的数据库角色的权限  
固定的服务器角色和固定的数据库角色的系统是源自 1980's年的旧系统。 固定的角色仍受支持，并可在其中有几个用户和安全需求是简单的环境中。 从 SQL Server 2005 开始，已创建的权限授予权限的更详细的系统。 此新系统是更精细，针对授予和拒绝的权限提供更多的选项。 更精细的系统的复杂性的增加，因此难以了解，但大多数企业系统应授予权限而不是使用固定的角色。 <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md). -->下图显示了与每个固定的数据库角色关联的权限。 此 SQL Server 图形中的所有权限不都是可用 （或必要） 在 AP 中。  
  
![APS 安全性固定数据库角色](./media/pdw-permissions/APS_security_fixed_db_roles.png "APS_security_fixed_db_roles")  
  
### <a name="related-content"></a>相关内容  
  
-   若要创建用户定义的角色，请参阅[CREATE ROLE](../t-sql/statements/create-role-transact-sql.md)。  
  
  
## <a name="fixed-server-roles"></a>固定服务器角色
SQL Server 会自动创建固定的服务器角色。 SQL Server PDW 具有有限的 SQL Server 固定服务器角色的成员实现。 仅**sysadmin**并**公共**具有作为成员的用户登录名。 **Setupadmin**并**dbcreator**角色内部使用的 SQL Server PDW。 无法添加或从任何角色中删除其他成员。  
  
### <a name="sysadmin-fixed-server-role"></a>sysadmin 固定服务器角色  
sysadmin 固定服务器角色的成员可以在服务器上执行任何活动  。 **Sa**登录名是唯一的成员**sysadmin**固定的服务器角色。 无法将其他登录名添加到**sysadmin**固定的服务器角色。 授予 CONTROL SERVER 权限近似拥有 sysadmin 固定服务器角色的成员身份   。 以下示例授予**CONTROL SERVER**到登录名的权限的名为 Fay。  
  
```sql  
USE master;  
GO  
GRANT CONTROL SERVER TO Fay;  
```  
  
> [!IMPORTANT]  
> **CONTROL SERVER**权限提供了几乎完全控制 SQL Server PDW。 只要有可能，请改为提供更加细化到登录名的权限。 例如，请考虑授予**VIEW SERVER STATE**， **ALTER ANY LOGIN**， **VIEW ANY DATABASE**，或者**CREATE ANY DATABASE**权限。  
  
### <a name="public-server-role"></a>公共服务器角色  
每个登录名可连接到 SQL Server PDW 是的成员**公共**服务器角色。 所有登录名继承授予的权限**公共**上任何对象。 只能将分配**公共**对象时所需的对象可供所有用户的权限。 不能更改中的成员身份**公共**角色。  
  
> [!NOTE]  
> **公共**实现方式与其他角色不同。 因为所有的服务器主体的公钥、 的成员身份成员**公共**角色中未列出**sys.server_role_members** DMV。  
  
### <a name="fixed-server-roles-vs-granting-permissions"></a>固定的服务器角色 vs。授予权限  
固定的服务器角色和固定的数据库角色的系统是源自 1980's年的旧系统。 固定的角色仍受支持，并可在其中有几个用户和安全需求是简单的环境中。 从 SQL Server 2005 开始，已创建的权限授予权限的更详细的系统。 此新系统是更精细，针对授予和拒绝的权限提供更多的选项。 更精细的系统的复杂性的增加，因此难以了解，但大多数企业系统应授予权限而不是使用固定的角色。 <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  -->  
  
## <a name="related-topics"></a>相关主题  
  
- [授予权限](grant-permissions.md)

<!-- MISSING LINKS
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->

