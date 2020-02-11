---
title: 权限
description: 本文介绍管理并行数据仓库的数据库权限的要求和选项。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: d60c6f492b0735e70a2c3103e48ad08953039adc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400873"
---
# <a name="managing-permissions-in-parallel-data-warehouse"></a>管理并行数据仓库中的权限
本文介绍用于管理 SQL Server PDW 的数据库权限的要求和选项。  
  
## <a name="BackupRestoreBasics"></a>数据库引擎权限基础知识  
SQL Server PDW 上的数据库引擎权限通过登录名在服务器级别进行管理，并通过数据库用户和用户定义的数据库角色在数据库级别进行管理。  
  
**登录名**  
登录名是用于登录到 SQL Server PDW 的单个用户帐户。 SQL Server PDW 使用 Windows 身份验证和 SQL Server 身份验证支持登录名。  Windows 身份验证登录名可以是受 SQL Server PDW 信任的任何域中的 Windows 用户或 Windows 组。 SQL Server 通过 SQL Server PDW 定义和验证身份验证登录名，并且必须通过指定密码进行创建。  
  
**Sysadmin**固定服务器角色的成员（如**sa**登录）可以连接到数据库，而无需映射到数据库用户。 它们将映射到**dbo**用户。 数据库的所有者也映射为**dbo**用户。  
  
**“服务器角色”**  
有四种特殊的服务器角色，其中包含一组预配置的角色，这些角色可提供便利的服务器级权限组。 **Sysadmin**、 **MediumRC**、 **LargeRC**和**XLargeRCfixed**服务器角色是当前在 SQL Server PDW 中实现的唯一服务器角色。 **Sa**登录名是**sysadmin**固定服务器角色的唯一成员，不能将其他登录名添加到**sysadmin**角色。 对于**sysadmin**固定服务器角色，可以向登录名授予**CONTROL SERVER**权限，这与此类似，但并不完全相同。 使用[ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md)将成员添加到其他服务器角色。 SQL Server PDW 不支持用户定义的服务器角色。  
  
**数据库用户**  
通过在数据库中创建数据库用户并将该数据库用户映射到登录名来授予登录名对数据库的访问权限。 通常，数据库用户名与登录名相同，尽管它不必要相同。 每个数据库用户均映射到单个登录名。 一个登录名只能映射到数据库中的一个用户，但可以映射为多个不同数据库中的数据库用户。  
  
**固定数据库角色**  
固定数据库角色是一组预配置的角色，可提供方便的数据库级权限组。 可以使用[sp_addrolemember](../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)过程将数据库用户和用户定义的数据库角色添加到固定数据库角色。 有关固定数据库角色的详细信息，请参阅[固定数据库角色](#fixed-database-roles)。  
  
**用户定义的数据库角色**  
具有 "**创建角色**" 权限的用户可以创建新的用户定义数据库角色，以表示具有常见权限的用户组。 通常对整个角色授予或拒绝权限，从而简化了权限管理和监视。  
  
使用**GRANT**语句向安全主体（登录名、用户和角色）授予权限。 使用 "**拒绝**" 命令显式拒绝权限。 使用**REVOKE**语句删除以前授予或拒绝的权限。 权限是累积的，用户将获得授予该用户、登录名和任何组成员身份的所有权限；但是任何权限拒绝将覆盖所有授予。 <!-- MISSING LINKS (For information, syntax, and available permissions with these commands, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md)).  -->  
  
下面的示例表示配置权限的常见和建议的方法。  
  
1.  如果使用 Windows 身份验证，则为每个要连接到 SQL Server PDW 的 Windows 用户或 Windows 组创建一个登录名。 如果使用 SQL Server 身份验证，则为将连接到 SQL Server PDW 的每个用户创建一个登录名。  
  
2.  为所有必要数据库中的每个登录名创建一个数据库用户。  
  
3.  创建一个或多个用户定义的数据库角色，每个角色表示一个类似的函数。 例如，财务分析人员和销售分析人员。  
  
4.  将数据库用户添加到一个或多个用户定义的数据库角色。  
  
5.  向用户定义的数据库角色授予权限。  
  
登录名是服务器级对象，可通过查看 sys.databases 来列出。 [server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)。 只能向服务器主体授予服务器级别权限。  
  
用户和数据库角色是数据库级对象，可通过查看 sys.databases 来列出。 [database_principals](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)。 只能向数据库主体授予数据库级权限。  
  
## <a name="BackupTypes"></a>默认权限  
以下列表对默认权限进行了说明：  
  
-   当使用**CREATE CREATE login**语句创建登录名时，登录名将收到**connect SQL**权限，允许登录名连接到 SQL Server PDW。  
  
-   当使用**CREATE user**语句创建数据库用户时，该用户将**在数据库：：<上收到 connect** _ database_name>_ 权限，允许登录名以用户身份连接到该数据库。  
  
-   默认情况下，所有主体（包括公共角色）都没有显式或隐式权限，因为隐式权限是从显式权限继承的。 因此，当不存在显式权限时，也可能没有隐式权限。  
  
-   当登录名成为对象或数据库的所有者时，该登录名始终具有对对象或数据库的所有权限。 所有权权限不作为显式权限显示。 **GRANT**、 **REVOKE**和**DENY**语句对所有权权限没有影响。 可以通过使用[ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md)语句更改所有权。  
  
-   sa 登录名具有设备上的所有权限。 类似于所有者权限，sa 权限无法更改，也不能显示为显式权限。 **GRANT**、 **REVOKE**和**DENY**语句对于 sa 权限不起作用。  
  
-   公共服务器角色默认情况下不接收权限，并且不从其他服务器角色继承权限。 可向公共服务器角色**授予 GRANT**、 **REVOKE**和**DENY**语句的显式权限。  
  
-   事务不需要权限。 所有主体都可以运行**BEGIN TRANSACTION**、 **COMMIT**和**ROLLBACK** TRANSACTION 命令。 但是，主体必须拥有适当的权限才能运行事务中的每个语句。  
  
-   USE 语句不需要权限****。 所有主体都可以对任何数据库运行**USE**语句，然而，若要访问数据库，必须在数据库中具有用户主体，或者必须启用来宾用户。  
  
### <a name="the-public-role"></a>公共角色  
所有新的设备登录名都将自动属于公共角色。 公共服务器角色具有以下特征：  
  
-   默认情况下，公共服务器角色没有权限。  
  
-   所有主体都是公共服务器角色的成员，而公共服务器角色不是另一个服务器角色的成员。  
  
-   公共服务器角色不能继承隐式权限。 授予 PUBLIC 角色的任何权限都必须显式授予。  
  
## <a name="BackupProc"></a>确定权限  
登录名是否具有执行特定操作的权限取决于为用户所属的登录名、用户和角色授予或拒绝的权限。 服务器级别的权限（如**创建登录名**和**查看服务器状态**）可用于服务器级主体（登录名）。 数据库级权限（如 "从表中**选择**" 或 "在过程中**执行**"）可用于数据库级主体（用户和数据库角色）。  
  
### <a name="implicit-and-explicit-permissions"></a>隐式和显式权限  
显式权限是 GRANT 或 DENY 语句给授予某主体的 GRANT 或 DENY 权限******************。 数据库级权限列在 " [sys. database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) " 视图中。 服务器级权限列在 " [sys. server_permissions](../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) " 视图中。  
  
*隐式权限*是主体（登录名或服务器角色）继承的**GRANT**或**DENY**权限。 可以通过以下方式继承权限。  
  
-   如果主体是角色的成员，即使主体没有显式**GRANT**或**DENY**权限，主体也可以从角色继承权限。  
  
-   如果主体对某个对象父作用域（如表的架构或对整个数据库的权限）拥有权限，则该主体可以继承对从属对象（如表）的权限。  
  
-   主体可以通过具有包含从属权限的权限来继承权限。 例如， **ALTER ANY USER**权限包含**CREATE user**和**ALTER ON USER：：** _<name>_ 权限。  
  
### <a name="determining-permissions-when-performing-actions"></a>在执行操作时确定权限  
确定要分配给主体的权限的过程是很复杂的。 确定隐式权限时会发生复杂性，因为主体可以是多个角色的成员，并且可以在角色层次结构中的多个级别传递权限。  
  
以下列表描述了用于确定权限的一般规则：  
  
-   所有权表示权限。  
  
    对象所有者对该对象具有所有权限。 同样，数据库所有者具有对数据库的所有权限以及对数据库中对象的所有权限。 不能更改这些权限。  
  
-   可以在服务器角色成员身份的层次结构中的多个级别继承权限。  
  
    例如，假设存在以下情况：  
  
    -   登录名 David 是数据库角色 PerfAnalysts 的成员。  
  
    -   PerfAnalysts 是数据库角色生产的成员。  
  
    -   David 和 PerfAnalysts 没有 Customer 表的**SELECT**权限。 权限已被吊销或从未显式授予。  
  
    -   生产对 Customer 表具有**SELECT**权限。  
  
    在这种情况下，PerfAnalysts 将从生产中继承 Customer 表的**grant**权限，而 David 会从生产中继承 customer 表的**授权**权限。  
  
-   **拒绝**替代在权限冲突时**授予**。  
  
    例如，假设登录名 David 没有 Customer 表的权限，并且是两个数据库角色的成员-dbgroup1 （对 Customer 表具有**DENY**权限）和 dbgroup2 （对 customer 表具有**GRANT**权限）。 在这种情况下，David 将继承 Customer 表的 "**拒绝**" 权限。 无论角色是显式获取权限还是隐式获取其权限，都是如此。  
  
### <a name="auditing-permissions"></a>审核权限  
若要调查用户的权限，请检查以下各项。  
  
-   执行以下查询以确定哪些登录名是系统管理员。  
  
    ```sql  
    SELECT SPLogins.name, 'is a member of ', SPRoles.name   
    FROM sys.server_role_members AS SRM   
    JOIN sys.server_principals AS SPRoles   
        ON SRM.role_principal_id = SPRoles.principal_id   
    JOIN sys.server_principals AS SPLogins   
        ON SRM.member_principal_id = SPLogins.principal_id;  
    ```  
  
-   执行以下查询以确定哪些登录名已被授予显式权限。  
  
    ```sql  
    SELECT name, 'has the ', state_desc , permission_name, ' permission'  
    FROM sys.server_permissions AS SP  
    JOIN sys.server_principals AS SPRoles   
        ON SP.grantee_principal_id = SPRoles.principal_id;  
    ```  
  
-   在用户数据库中执行以下查询，以确定哪些数据库用户是数据库角色的成员。  
  
    ```sql  
    SELECT DPUsers.name, 'is a member of ', DPRoles.name    
    FROM sys.database_role_members AS DRM  
    JOIN sys.database_principals AS DPRoles   
        ON DRM.role_principal_id = DPRoles.principal_id  
    JOIN sys.database_principals AS DPUsers  
        ON DRM.member_principal_id = DPUsers.principal_id;  
    ```  
  
-   在用户数据库中执行以下查询，以确定哪些数据库用户和角色已被授予或拒绝特定权限。 你将需要查询其他视图（如 sys.databases 和 sys.databases）来标识与 major_id 描述的项目。  
  
    ```sql  
    SELECT DPUsers.name, 'has the ', permission_name,   
    'permission on the item described as class = ', class, 'id = ', major_id  
    FROM sys.database_permissions AS DP  
    JOIN sys.database_principals AS DPUsers  
        ON DP.grantee_principal_id = DPUsers.principal_id;  
    ```  
  
## <a name="RestoreProc"></a>数据库权限最佳做法  
  
-   以最精细的级别授予权限。 向表或视图级别授予权限可能会变得不受管理。 但在数据库级别授予权限可能会过于宽松。 如果数据库是使用架构来定义的，则可能是授予架构的权限在表级别和数据库级别之间具有适当的折衷。  
  
-   向角色而不是用户或登录名授予权限。 通过使用角色而不是用户来管理权限，可以通过将用户或登录名移入或移出角色来轻松地为其快速授予或撤消一组权限。 当函数从一个用户传递到另一个用户时，权限在角色成员身份更改时可以保持不变。  
  
-   基于作业功能向角色授予权限，并在更高级别的组角色上根据执行操作的公司组来合并作业职能角色。  
  
-   每个最终用户都应具有唯一的登录名。 不允许用户共享登录名。 为每个用户提供一个登录名可确保审核记录并简化权限管理。  
  
## <a name="fixed-database-roles"></a>固定数据库角色
SQL Server 提供预配置（固定）数据库级角色，以帮助你管理服务器上的权限。 预先配置的角色是固定的，因为你无法更改分配给它们的权限。 还可以创建用户定义的数据库角色。 您可以更改分配给用户定义的数据库角色的权限。  
  
角色是对其他主体进行分组的安全主体。 数据库角色在其权限范围内是数据库范围内的。 数据库用户和其他数据库角色可以添加为数据库角色的成员。 固定数据库角色无法添加到对方。 （“角色”** 类似于 Windows 操作系统中的“组”**。）  
  
有9个固定数据库角色。  
  
-   **db_owner**  
  
-   **db_securityadmin**  
  
-   **db_accessadmin**  
  
-   **db_backupoperator**  
  
-   **db_ddladmin**  
  
-   **db_datawriter**  
  
-   **db_datareader**  
  
-   **db_denydatawriter**  
  
-   **db_denydatareader**  
  
### <a name="permissions-of-the-fixed-database-roles"></a>固定数据库角色的权限  
固定服务器角色的系统和固定数据库角色的系统是在1980年产生的旧系统。 固定角色仍受支持，并且在具有很少用户和安全需求的环境中非常有用。 从 SQL Server 2005 开始，创建了更详细的授权权限系统。 这个新系统更为精细，提供了更多选项用于授予和拒绝权限。 更精细的系统的额外复杂性使得更难学习，但大多数企业系统应授予权限，而不是使用固定角色。 <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md). -->下图显示了与每个固定数据库角色关联的权限。 此 SQL Server 图形中的所有权限在 AP 中均不可用（或必需）。  
  
![APS 安全性固定数据库角色](./media/pdw-permissions/APS_security_fixed_db_roles.png "APS_security_fixed_db_roles")  
  
### <a name="related-content"></a>相关内容  
  
-   若要创建用户定义的角色，请参阅[创建角色](../t-sql/statements/create-role-transact-sql.md)。  
  
  
## <a name="fixed-server-roles"></a>固定服务器角色
固定服务器角色由 SQL Server 自动创建。 SQL Server PDW 具有 SQL Server 固定服务器角色的有限实现。 只有**sysadmin**和**public**具有用户登录名作为成员。 **Setupadmin**和**dbcreator**角色由 SQL Server PDW 在内部使用。 不能在任何角色中添加或删除其他成员。  
  
### <a name="sysadmin-fixed-server-role"></a>sysadmin 固定服务器角色  
sysadmin 固定服务器角色的成员可以在服务器上执行任何活动****。 **Sa**登录名是**sysadmin**固定服务器角色的唯一成员。 不能将其他登录名添加到**sysadmin**固定服务器角色。 授予 CONTROL SERVER 权限近似拥有 sysadmin 固定服务器角色的成员身份********。 下面的示例向**CONTROL SERVER**授予对名为 Fay 的登录名的权限。  
  
```sql  
USE master;  
GO  
GRANT CONTROL SERVER TO Fay;  
```  
  
> [!IMPORTANT]  
> **CONTROL SERVER**权限几乎可以完全控制 SQL Server PDW。 请尽可能为登录提供更详细的权限。 例如，请考虑授予**查看服务器状态**、**更改任何登录名**、**查看任何数据库**或**创建任何数据库**权限。  
  
### <a name="public-server-role"></a>公共服务器角色  
可以连接到 SQL Server PDW 的每个登录名都是**public**服务器角色的成员。 所有登录名都将继承在任何对象上授予**public**的权限。 仅当要将对象提供给所有用户时，才在对象上分配**public**权限。 不能更改**公共**角色的成员身份。  
  
> [!NOTE]  
> **public**的实现方式与其他角色不同。 由于所有服务器主体都是公共角色的成员，因此不会在**sys. server_role_members** DMV 中列出**public**角色的成员身份。  
  
### <a name="fixed-server-roles-vs-granting-permissions"></a>固定服务器角色与授予权限  
固定服务器角色的系统和固定数据库角色的系统是在1980年产生的旧系统。 固定角色仍受支持，并且在具有很少用户和安全需求的环境中非常有用。 从 SQL Server 2005 开始，创建了更详细的授权权限系统。 这个新系统更为精细，提供了更多选项用于授予和拒绝权限。 更精细的系统的额外复杂性使得更难学习，但大多数企业系统应授予权限，而不是使用固定角色。 <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  -->  
  
## <a name="related-topics"></a>相关主题  
  
- [授予权限](grant-permissions.md)

<!-- MISSING LINKS
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->

