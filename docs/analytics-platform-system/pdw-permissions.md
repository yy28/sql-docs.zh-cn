---
title: 并行数据仓库中的权限 |Microsoft 文档
description: 本文介绍的要求和用于管理并行数据仓库的数据库权限的选项。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 16ed81d3349cd1e641a66a95d9993e2a86ca4098
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
ms.locfileid: "31544879"
---
# <a name="managing-permissions-in-parallel-data-warehouse"></a>并行数据仓库中的管理权限
本文介绍的要求和用于管理 SQL Server PDW 的数据库权限的选项。  
  
## <a name="BackupRestoreBasics"></a>数据库引擎权限基础知识  
SQL Server PDW 上的数据库引擎权限管理服务器级别通过登录名，并在数据库级别通过数据库用户和用户定义的数据库角色。  
  
**登录名**  
登录名是用于登录到 SQL Server PDW 的单个用户帐户。 SQL Server PDW 支持使用 Windows 身份验证和 SQL Server 身份验证的登录名。  Windows 身份验证登录名可以是 Windows 用户或通过 SQL Server PDW 受信任的任何域的 Windows 组。 SQL Server 身份验证登录名定义并由 SQL Server PDW 进行身份验证，必须创建通过指定密码。  
  
成员**sysadmin**固定的服务器角色 (如**sa**登录名) 而无映射到数据库用户可以连接到数据库。 它们将映射到**dbo**用户。 数据库的所有者还映射为**dbo**用户。  
  
**服务器角色**  
有个一组预配置提供方便组的服务器级权限的角色的四个特殊的服务器角色。 **Sysadmin**， **MediumRC**， **LargeRC**，和**XLargeRCfixed**服务器角色是当前实现在 SQL 中唯一的服务器角色Server PDW。 **Sa**登录名是唯一的成员**sysadmin**固定的服务器角色和其他登录名不能添加到**sysadmin**角色。 可以授予登录名**CONTROL SERVER**权限，这是类似，但并不相同，到**sysadmin**固定的服务器角色。 使用[ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md)将成员添加到其他服务器角色。 SQL Server PDW 不支持用户定义的服务器角色。  
  
**数据库用户**  
登录帐户已通过的数据库中创建的数据库用户并将该数据库用户映射到登录名授予对数据库的访问。 通常，数据库用户名与登录名相同，尽管它不必要相同。 每个数据库用户均映射到单个登录名。 一个登录名只能映射到数据库中的一个用户，但可以映射为多个不同数据库中的数据库用户。  
  
**固定的数据库角色**  
固定的数据库角色是提供方便组的数据库级权限的预配置的角色的一组。 数据库用户和用户定义的数据库角色可以添加到固定的数据库角色使用[sp_addrolemember](../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)过程。 有关固定的数据库角色的详细信息，请参阅[固定数据库角色](#fixed-database-roles)。  
  
**用户定义的数据库角色**  
使用用户**创建角色**权限可以创建新的用户定义的数据库角色来表示具有常用权限的用户组。 通常对整个角色授予或拒绝权限，从而简化了权限管理和监视。  
  
向安全主体 （登录名、 用户和角色） 授予权限，应使用**授予**语句。 通过使用显式拒绝权限**拒绝**命令。 使用删除以前授予或拒绝权限**撤消**语句。 权限是累积的，用户将获得授予该用户、登录名和任何组成员身份的所有权限；但是任何权限拒绝将覆盖所有授予。 <!-- MISSING LINKS (For information, syntax, and available permissions with these commands, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md)).  -->  
  
下面的示例表示配置权限的常见和建议的方法。  
  
1.  如果使用 Windows 身份验证，则创建每个 Windows 用户或 Windows 组将连接到 SQL Server PDW 的一个登录名。 如果使用 SQL Server 身份验证，则会将连接到 SQL Server PDW 的每个人创建登录名。  
  
2.  创建所有必要的数据库中的每个登录名的数据库用户。  
  
3.  创建一个或多个用户定义的数据库角色，每个表示相似的职能。 例如，财务分析人员和销售分析人员。  
  
4.  将数据库用户添加到一个或多个用户定义的数据库角色。  
  
5.  向用户定义的数据库角色授予权限。  
  
登录名是服务器级对象，可以通过查看列出[sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)。 只有服务器级别权限可以授予服务器主体。  
  
用户和数据库角色是数据库级别对象，可以通过查看列出[sys.database_principals](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)。 仅数据库级权限可以授予数据库主体。  
  
## <a name="BackupTypes"></a>默认权限  
以下列表对默认权限进行了说明：  
  
-   Using 创建登录名时**CREATE LOGIN**语句，该登录名接收**CONNECT SQL**允许登录的权限连接到 SQL Server PDW。  
  
-   通过使用创建数据库用户时**CREATE USER**语句中，用户会收到 **连接 ON DATABASE:: * * * < s e _ >* 权限，允许连接到该数据库的登录名作为的用户。  
  
-   因为从显式权限继承的隐式权限，所有主体，包括 PUBLIC 角色，默认情况下有任何显式或隐式权限。 因此，当存在任何显式权限不时，还有其他任何隐式权限。  
  
-   当登录名变为对象或数据库的所有者时，该登录名始终具有对对象或数据库的所有权限。 所有权权限并不显示为显式权限。 **授予**，**撤消**，和**拒绝**语句具有所有权权限没有影响。 可以使用更改所有权[ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md)语句。  
  
-   Sa 登录名在设备上具有所有权限。 类似于所有权的权限，sa 权限不能更改，并不显示为显式权限。 **授予**，**撤消**，和**拒绝**语句具有 sa 权限没有影响。  
  
-   PUBLIC 服务器角色默认情况下接收任何权限，并不从其他服务器角色继承权限。 PUBLIC 服务器角色可以提供与显式权限**授予**，**撤消**，和**拒绝**语句。  
  
-   事务不需要的权限。 可以运行所有主体**BEGIN TRANSACTION**，**提交**，和**回滚**事务命令。 但是，主体必须具有运行在事务中的每个语句的适当权限。  
  
-   USE 语句不需要权限。 可以运行所有主体**使用**语句上任何数据库，但若要访问数据库它们必须用户主体拥有数据库中，或者必须启用了 guest 用户。  
  
### <a name="the-public-role"></a>公共角色  
所有新的设备登录名自动属于 PUBLIC 角色。 PUBLIC 服务器角色具有以下特征：  
  
-   默认情况下，PUBLIC 服务器角色具有任何权限。  
  
-   所有主体都是 PUBLIC 服务器角色的成员，PUBLIC 服务器角色不是另一个服务器角色的成员。  
  
-   PUBLIC 服务器角色不能继承隐式权限。 必须显式授予公共角色授予任何权限。  
  
## <a name="BackupProc"></a>确定权限  
登录名有权执行特定的操作取决于授予或拒绝登录名、 用户和用户角色的成员的权限。 服务器级权限 (如**CREATE LOGIN**和**VIEW SERVER STATE**) 可供服务器级别主体 （登录名）。 数据库级别权限 (如**选择**从表或**执行**对过程) 可供数据库级主体 （用户和数据库角色）。  
  
### <a name="implicit-and-explicit-permissions"></a>隐式和显式权限  
显式权限是 GRANT 或 DENY 语句给授予某主体的 GRANT 或 DENY 权限。 中列出了数据库级别权限[sys.database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)视图。 中列出了服务器级权限[sys.server_permissions](../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)视图。  
  
*隐式权限*是**授予**或**拒绝**主体 （登录名或服务器角色） 已继承的权限。 可以通过以下方式继承权限。  
  
-   主体可以继承权限从角色如果主体数据库角色的成员，即使主体没有显式**授予**或**拒绝**权限。  
  
-   如果主体具有对某个对象父作用域 （如表或整个数据库的权限的架构） 的权限，则主体可以继承从属的对象 （如表） 的权限。  
  
-   主体可以具有的权限，包括从属权限继承权限。 例如**ALTER ANY USER**权限包括**CREATE USER**和 **ALTER ON USER:: * * *<name>* 权限。  
  
### <a name="determining-permissions-when-performing-actions"></a>执行操作时确定权限  
确定要分配给主体的权限复杂的过程。 确定隐式权限，因为主体可以是多个角色的成员和权限可以通过角色层次结构中的多个级别时发生复杂性。  
  
以下列表描述用于确定权限的一般规则：  
  
-   所有权隐含权限。  
  
    对象所有者对象上具有所有权限。 同样，数据库所有者具有在数据库上的所有权限和对对象的所有权限在数据库中。 无法更改这些权限。  
  
-   可以跨多个服务器角色成员资格的层次结构中的级别继承的权限。  
  
    例如，假设有以下情况：  
  
    -   登录名 David 是数据库角色 PerfAnalysts 的成员。  
  
    -   PerfAnalysts 是数据库角色生产的成员。  
  
    -   David 和 PerfAnalysts 没有**选择**Customer 表中的权限。 权限已吊销或永远不会显式授予。  
  
    -   生产具有**选择**Customer 表中的权限。  
  
    在这种情况下，将继承 PerfAnalysts**授予**从生产环境和 David Customer 表中的权限将继承**授予**在生产中的客户表上的权限。  
  
-   **拒绝**重写**授予**权限发生冲突时。  
  
    例如，假设登录 David Customer 表中具有任何权限，并且是两个数据库角色的成员 – dbgroup1，具有**拒绝**权限的客户表和 dbgroup2，具有**授予**Customer 表的权限。 在这种情况下，将继承 David**拒绝**Customer 表中的权限。 是否显式或隐式，角色获得其权限，这种情况。  
  
### <a name="auditing-permissions"></a>审核权限  
若要检索用户的权限，请检查以下。  
  
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
  
-   在用户数据库以确定哪些数据库用户是数据库角色的成员执行以下查询。  
  
    ```sql  
    SELECT DPUsers.name, 'is a member of ', DPRoles.name    
    FROM sys.database_role_members AS DRM  
    JOIN sys.database_principals AS DPRoles   
        ON DRM.role_principal_id = DPRoles.principal_id  
    JOIN sys.database_principals AS DPUsers  
        ON DRM.member_principal_id = DPUsers.principal_id;  
    ```  
  
-   在用户数据库来确定同意或拒绝的特定权限的数据库用户和角色执行以下查询。 你将需要在查询其他视图，例如 sys.objects 和 sys.schemas 标识与 major_id 所述的项目。  
  
    ```sql  
    SELECT DPUsers.name, 'has the ', permission_name,   
    'permission on the item described as class = ', class, 'id = ', major_id  
    FROM sys.database_permissions AS DP  
    JOIN sys.database_principals AS DPUsers  
        ON DP.grantee_principal_id = DPUsers.principal_id;  
    ```  
  
## <a name="RestoreProc"></a>数据库权限最佳实践  
  
-   授予权限是可行的在最高粒度级别。 授予在表或视图级别的权限可能会变得难以管理。 但在数据库级别授予权限可能会太宽松。 如果数据库具有架构用于定义工作边界，可能对架构的授予权限是表级别和数据库级别之间了适当的折衷。  
  
-   授予权限给角色，而不是用户或登录名。 通过使用角色而不用户管理权限，使得容易快速授予或撤销通过将它们移入 （出） 角色的一组用户或登录名的权限。 何时函数从一个人员传递到另一个，权限可以保持不变在角色级别的角色成员身份更改时。  
  
-   向角色授予权限基于作业函数，并基于组合根据公司组执行操作的作业函数角色的更高级别的组角色。  
  
-   每个最终用户应具有唯一的登录名。 不允许用户共享登录名。 为每个用户提供登录名可确保审核记录，并且简化了权限管理。  
  
## <a name="fixed-database-roles"></a>固定数据库角色
SQL Server 提供了预配置的 （固定） 数据库级角色，来帮助你管理的服务器上的权限。 预配置的角色被固定的因为无法更改分配给他们的权限。 也可以创建用户定义的数据库角色。 你可以更改分配给用户定义的数据库角色的权限。  
  
角色是可组合其他主体的安全主体。 数据库角色是数据库范围内其权限作用域中。 可以作为数据库角色的成员添加数据库用户和其他数据库角色。 无法将固定的数据库角色添加到对方。 （“角色”类似于 Windows 操作系统中的“组”。）  
  
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
固定的服务器角色和固定的数据库角色的系统是来源于 1980's年旧系统。 固定的角色仍受支持，并在其中有几个用户，安全需求是简单的环境中有用。 从 SQL Server 2005 开始，已创建授予权限的更详细的系统。 此新系统是更精细，同时授予和拒绝权限为提供更多的选项。 更精细的系统的额外复杂性使更难若要了解，但大多数企业系统应授予权限而不是使用固定的角色。 <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md). -->下图显示了与每个固定的数据库角色的权限。 此 SQL Server 图形中的所有权限不都是可用 （或需要） 访问点中。  
  
![固定数据库角色的 AP 安全](./media/pdw-permissions/APS_security_fixed_db_roles.png "APS_security_fixed_db_roles")  
  
### <a name="related-content"></a>相关内容  
  
-   若要创建用户定义的角色，请参阅[创建角色](../t-sql/statements/create-role-transact-sql.md)。  
  
  
## <a name="fixed-server-roles"></a>固定服务器角色
SQL Server 自动创建固定的服务器角色。 SQL Server PDW 具有 SQL Server 固定服务器角色的有限的实现。 仅**sysadmin**和**公共**具有作为成员的用户登录名。 **Setupadmin**和**dbcreator**角色内部使用的 SQL Server PDW。 无法添加或从任何角色中删除其他成员。  
  
### <a name="sysadmin-fixed-server-role"></a>sysadmin 固定服务器角色  
sysadmin 固定服务器角色的成员可以在服务器上执行任何活动。 **Sa**登录名是唯一的成员**sysadmin**固定的服务器角色。 无法将其他登录名添加到**sysadmin**固定的服务器角色。 授予 CONTROL SERVER 权限近似拥有 sysadmin 固定服务器角色的成员身份。 下面的示例授予**CONTROL SERVER**登录名具有权限的名为 Fay。  
  
```sql  
USE master;  
GO  
GRANT CONTROL SERVER TO Fay;  
```  
  
> [!IMPORTANT]  
> **CONTROL SERVER**权限提供的 SQL Server PDW 几乎完全控制。 只要有可能，请改为提供更为细化到登录名的权限。 例如，考虑授予**VIEW SERVER STATE**， **ALTER ANY LOGIN**， **VIEW ANY DATABASE**，或**CREATE ANY DATABASE**权限。  
  
### <a name="public-server-role"></a>public 服务器角色  
可以连接到 SQL Server PDW 每个登录名为属于**公共**服务器角色。 所有登录名继承授予的权限**公共**任何对象。 仅分配**公共**对象时想要对象可供所有用户的权限。 无法更改中的成员身份**公共**角色。  
  
> [!NOTE]  
> **公共**不同于其他角色实现。 因为所有的服务器主体的公钥、 的成员身份的成员**公共**中未列出角色**sys.server_role_members** DMV。  
  
### <a name="fixed-server-roles-vs-granting-permissions"></a>固定的服务器角色 vs。授予权限  
固定的服务器角色和固定的数据库角色的系统是来源于 1980's年旧系统。 固定的角色仍受支持，并在其中有几个用户，安全需求是简单的环境中有用。 从 SQL Server 2005 开始，已创建授予权限的更详细的系统。 此新系统是更精细，同时授予和拒绝权限为提供更多的选项。 更精细的系统的额外复杂性使更难若要了解，但大多数企业系统应授予权限而不是使用固定的角色。 <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  -->  
  
## <a name="related-topics"></a>相关主题  
  
- [授予权限](grant-permissions.md)

<!-- MISSING LINKS
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->

