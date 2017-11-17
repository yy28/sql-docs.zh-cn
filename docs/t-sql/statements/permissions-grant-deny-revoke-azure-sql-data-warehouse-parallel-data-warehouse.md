---
title: "授予拒绝撤消 Perms Azure SQL 数据和并行数据仓库 |Microsoft 文档"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5a3b7424-408e-4cb0-8957-667ebf4596fc
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3c4beb3881b983c0af3add7671dc4c7155649497
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse"></a>权限： GRANT、 DENY、 REVOKE （Azure SQL 数据仓库，并行数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  使用[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]**授予**和**拒绝**语句来授予或拒绝权限 (如**更新**) 对安全对象 （如数据库、 表、 视图等等。)向安全主体 （登录名、 数据库用户或数据库角色）。 使用**撤消**删除授予或拒绝的权限。  
  
 服务器级别权限适用于登录名。 数据库级别权限适用于数据库用户和数据库角色。  
  
 若要查看哪些权限已授予和拒绝，查询的 sys.server_permissions 和 sys.database_permissions 视图。 可以由采用具有权限的角色的成员资格继承权限未显式授予或拒绝对安全主体。 固定的数据库角色的权限不能更改，并不会出现在 sys.server_permissions 和 sys.database_permissions 视图。  
  
-   **授予**显式授予一个或多个权限。  
  
-   **拒绝**显式具有一个或多个权限将拒绝主体。  
  
-   **撤消**会删除存在**授予**或**拒绝**权限。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
GRANT   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    TO principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
[;]  
  
DENY   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    TO principal [ ,...n ]  
    [ CASCADE ]  
[;]  
  
REVOKE   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    [ FROM | TO ] principal [ ,...n ]  
    [ CASCADE ]  
[;]  
  
<permission> ::=  
{ see the tables below }  
  
<class_type> ::=  
{  
      LOGIN  
    | DATABASE  
    | OBJECT  
    | ROLE  
    | SCHEMA  
    | USER  
}  
```  
  
## <a name="arguments"></a>参数  
 \<权限 > [ **，**...*n* ]  
 一个或多个权限授予、 拒绝或撤消。  
  
 ON [ \<class_type >::]*安全* **ON**子句描述用于授予、 拒绝或撤消权限的安全对象参数。  
  
 \<class_type > 的安全对象的类类型。 这可以是**登录**，**数据库**，**对象**，**架构**，**角色**，或**用户**. 此外可授予权限**服务器***class_type*，但**服务器**未指定这些权限。 **数据库**未指定时权限包括单词**数据库**(例如**ALTER ANY DATABASE**)。 如果没有*class_type*指定和权限类型并不局限于服务器或数据库类，该类假定为**对象**。  
  
 *安全对象*  
 登录名、 数据库、 表、 视图、 架构、 过程、 角色或授予，所依据的用户的名称拒绝或撤消权限。 可以使用中所述的由三部分命名规则指定的对象名称[TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
 到*主体*[ **，**...*n* ]  
 一个或多个主体授予、 拒绝或撤消权限。 主体是登录名、 数据库用户或数据库角色的名称。  
  
 从*主体*[ **，**...*n* ]  
 若要撤消的权限的一个或多个主体。  主体是登录名、 数据库用户或数据库角色的名称。 **从**只能与使用**撤消**语句。 **到**可以与使用**授予**，**拒绝**，或**撤消**。  
  
 WITH GRANT OPTION  
 指示被授权者在获得指定权限的同时还可以将指定权限授予其他主体。  
  
 CASCADE  
 指示权限是拒绝或撤消对指定的主体和向主体授予权限的所有其他主体。 在主体拥有使用权限时需要**GRANT 选项**。  
  
 GRANT OPTION FOR  
 指示将撤消授予指定权限的能力。 这是必需的当你使用**CASCADE**自变量。  
  
> [!IMPORTANT]  
>  如果主体拥有指定的权限而无需**授予**选项，将吊销本身的权限。  
  
## <a name="permissions"></a>Permissions  
 若要授予权限，授权者必须具有自身的任一权限与**WITH GRANT OPTION**，或者必须具有隐含授予该权限更高权限。  对象所有者可以授予对其所拥有的对象的权限。 具有主体**控件**对安全对象的权限可以授予权限，在该安全对象。  成员**db_owner**和**db_securityadmin**固定的数据库角色可以授予数据库中的任何权限。  
  
## <a name="general-remarks"></a>一般备注  
 拒绝或撤消向主体的权限将不会影响已通过授权和当前运行的请求。 若要限制访问立即，你必须取消活动请求或终止当前会话。  
  
> [!NOTE]  
>  最固定的服务器角色不是此版本中可用的。 改为使用用户定义的数据库角色。 无法将登录名添加到**sysadmin**固定的服务器角色。 授予**CONTROL SERVER**权限总数接近于中的成员身份**sysadmin**固定的服务器角色。  
  
 某些语句需要多种权限。 例如，若要创建表需要**CREATE TABLE**在数据库中，权限和**ALTER SCHEMA**将包含表的表的权限。  
  
 PDW 有时执行存储的过程将分发到计算节点的用户操作。 因此，不能对整个数据库的 execute 权限被拒绝。 (例如`DENY EXECUTE ON DATABASE::<name> TO <user>;`将失败。)作为替代，拒绝对特定对象 （过程） 或用户架构的 execute 权限。  
  
### <a name="implicit-and-explicit-permissions"></a>隐式和显式权限  
 *显式权限*是**授予**或**拒绝**向通过主体授予的权限**授予**或**拒绝**语句。  
  
 *隐式权限*是**授予**或**拒绝**主体 （登录名、 用户或数据库角色） 已从另一个数据库角色继承的权限。  
  
 隐式权限还可以从覆盖或父权限继承。 例如，**更新**对表的权限可以继承通过让**更新**上包含的表的架构的权限或**控件**对表的权限。  
  
### <a name="ownership-chaining"></a>所有权链接  
 当多个数据库对象按顺序相互访问时，该序列称为*链*。 尽管这样的链不会单独存在，但是当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 遍历链中的链接时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 评估对构成对象的权限时的方式与单独访问对象时不同。 所有权链接具有重要的意义，用于管理安全性。 有关所有权链的详细信息，请参阅[所有权链](http://msdn.microsoft.com/en-us/library/ms188676\(v=sql11\).aspx)和[教程： 所有权链和上下文切换](http://msdn.microsoft.com/en-us/library/bb153640\(v=sql11\).aspx)。  
  
## <a name="permission-list"></a>权限列表  
  
### <a name="server-level-permissions"></a>服务器级别权限  
 服务器级别权限可以授予、 拒绝，并吊销从登录名。  
  
 **将应用到服务器的权限**  
  
-   CONTROL SERVER  
  
-   ADMINISTER BULK OPERATIONS  
  
-   ALTER ANY CONNECTION  
  
-   ALTER ANY DATABASE  
  
-   CREATE ANY DATABASE  
  
-   ALTER ANY EXTERNAL DATA SOURCE  
  
-   ALTER ANY EXTERNAL FILE FORMAT  
  
-   ALTER ANY LOGIN  
  
-   ALTER SERVER STATE  
  
-   CONNECT SQL  
  
-   VIEW ANY DEFINITION  
  
-   VIEW ANY DATABASE  
  
-   VIEW SERVER STATE  
  
 **适用于登录名的权限**  
  
-   在登录控制  
  
-   ALTER 登录  
  
-   模拟登录  
  
-   VIEW DEFINITION  
  
### <a name="database-level-permissions"></a>数据库级别权限  
 数据库级别权限可以授予，被拒绝，和吊销从数据库用户和用户定义的数据库角色。  
  
 **适用于所有数据库类的权限**  
  
-   CONTROL  
  
-   ALTER  
  
-   VIEW DEFINITION  
  
 **适用于除用户外的所有数据库类的权限**  
  
-   TAKE OWNERSHIP  
  
 **仅适用于数据库的权限**  
  
-   ALTER ANY DATABASE  
  
-   更改数据库上  
  
-   ALTER ANY DATASPACE  
  
-   ALTER ANY ROLE  
  
-   ALTER ANY SCHEMA  
  
-   ALTER ANY USER  
  
-   BACKUP DATABASE  
  
-   在数据库上连接  
  
-   CREATE PROCEDURE  
  
-   CREATE ROLE  
  
-   CREATE SCHEMA  
  
-   CREATE TABLE  
  
-   CREATE VIEW  
  
-   SHOWPLAN  
  
 **仅适用于用户的权限**  
  
-   IMPERSONATE  
  
 **将应用于数据库、 架构和对象的权限**  
  
-   ALTER  
  
-   DELETE  
  
-   EXECUTE  
  
-   Insert  
  
-   SELECT  
  
-   UPDATE  
  
-   引用  
  
 有关每种类型的权限的定义，请参阅[权限 （数据库引擎）](http://msdn.microsoft.com/library/ms191291.aspx)。  
  
### <a name="chart-of-permissions"></a>权限的图表  
 此海报上以图形方式表示的所有权限。 这是查看的权限的嵌套层次结构的最简单方法。 例如**ALTER ON LOGIN**权限可授予其本身而言，但如果授予登录名，它会还包含**控件**权限对该登录名，或如果授予登录名**ALTER ANY登录名**权限。  
  
 ![AP 安全权限海报](../../t-sql/statements/media/aps-security-perms-poster.png "AP 安全权限海报")  
  
 若要下载该海报的全尺寸版本，请参阅[SQL Server PDW 权限](http://go.microsoft.com/fwlink/?LinkId=244249)AP Yammer 站点的文件部分中 (或通过从电子邮件请求 **apsdoc@microsoft.com** 。  
  
## <a name="default-permissions"></a>默认权限  
 以下列表描述了默认权限：  
  
-   当通过使用创建一个登录名**CREATE LOGIN**语句新登录名接收**CONNECT SQL**权限。  
  
-   所有登录名都属于**公共**服务器角色并且不能删除从**公共**。  
  
-   通过使用创建数据库用户时**CREATE USER**权限，数据库用户会收到**连接**数据库中的权限。  
  
-   包括的所有主体**公共**角色，默认情况下有任何显式或隐式权限。  
  
-   当登录名或用户将成为数据库或对象的所有者时，登录名或用户始终具有在数据库或对象上的所有权限。 所有权权限不能更改并且不显示为显式权限。 **授予**，**拒绝**，和**撤消**语句具有所有者没有影响。  
  
-   **Sa**登录名在设备上具有所有权限。 类似于所有权权限**sa**权限不能更改，并不显示为显式权限。 **授予**，**拒绝**，和**撤消**语句不起任何作用**sa**登录名。 **Sa**登录名不能重命名。  
  
-   **使用**语句不需要权限。 可以运行所有主体**使用**对任何数据库的语句。  
  
##  <a name="Examples"></a>示例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-granting-a-server-level-permission-to-a-login"></a>A. 授予向登录名的服务器级权限  
 下面的两个语句授予到登录名的服务器级权限。  
  
```  
GRANT CONTROL SERVER TO [Ted];  
```  
  
```  
GRANT ALTER ANY DATABASE TO Mary;  
```  
  
### <a name="b-granting-a-server-level-permission-to-a-login"></a>B. 授予向登录名的服务器级权限  
 下面的示例授予登录名添加到的服务器主体 （另一个登录名） 上的服务器级权限。  
  
```  
GRANT  VIEW DEFINITION ON LOGIN::Ted TO Mary;  
```  
  
### <a name="c-granting-a-database-level-permission-to-a-user"></a>C. 向用户授予数据库级别权限  
 下面的示例授予一名用户访问数据库主体 （另一个用户） 上的数据库级权限。  
  
```  
GRANT VIEW DEFINITION ON USER::[Ted] TO Mary;  
```  
  
### <a name="d-granting-denying-and-revoking-a-schema-permission"></a>D. 授予、 拒绝和撤消架构权限  
 以下**授予**语句授予 Yuen 从任何表或在 dbo 架构视图中选择数据的功能。  
  
```  
GRANT SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 以下**拒绝**语句可以防止 Yuen 选择从任何表或视图 dbo 架构中的数据。 Yuen 无法读取数据，即使他具有权限以某种其他方式，例如通过角色成员身份。  
  
```  
DENY SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 以下**撤消**语句中删除**拒绝**权限。 现在不中性 Yuen 的显式权限。 Yuen 可能能够从通过某些其他隐式的权限，如角色成员身份的任何表中选择数据。  
  
```  
REVOKE SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
### <a name="e-demonstrating-the-optional-object-clause"></a>E. 演示的可选对象:: 子句  
 对象是权限语句的默认类，因为以下两个语句是相同的。 **对象::**子句是可选的。  
  
```  
GRANT UPDATE ON OBJECT::dbo.StatusTable TO [Ted];  
```  
  
```  
GRANT UPDATE ON dbo.StatusTable TO [Ted];  
```  
  
  


