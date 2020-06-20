---
title: 创建数据库用户 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.DATABASEUSER.GENERAL.F1
- sql12.swb.user.securables.f1
helpviewer_keywords:
- database users, creating
- creating users with Management Studio
- mapping users
- users [SQL Server], creating
- database user additions [SQL Server]
- database users, mapping
- CREATE USER [Management Studio]
- users [SQL Server], adding
- mapping database users
ms.assetid: 782798d3-9552-4514-9f58-e87be4b264e4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 97fc758c754f5fc8803e988d55147670fc3ff45b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055437"
---
# <a name="create-a-database-user"></a>创建数据库用户
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中创建映射到某一登录名的数据库用户。 数据库用户是连接到数据库时的登录名的标识。 数据库用户可以使用与登录名相同的名称，但这不是必需的。 本主题假设 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中已存在登录名。 有关如何创建登录名的信息，请参阅[创建登录名](create-a-login.md)。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [背景](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要创建数据库用户，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="background"></a><a name="Restrictions"></a> 背景  
 用户是数据库级别安全主体。 登录名必须映射到数据库用户才能连接到数据库。 一个登录名可以作为不同用户映射到不同的数据库，但在每个数据库中只能作为一个用户进行映射。 在部分包含数据库中，可以创建不具有登录名的用户。 有关包含的数据库用户的详细信息，请参阅 [CREATE USER (Transact-SQL)](/sql/t-sql/statements/create-user-transact-sql)。 如果在数据库中启用了 guest 用户，未映射到数据库用户的登录名可作为 guest 用户进入该数据库。  
  
> [!IMPORTANT]  
>  guest 用户通常处于禁用状态。 除非有必要，否则不要启用 guest 用户。  
  
 可以向作为安全主体的用户授予权限。 用户的作用域是数据库。 若要连接 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例上的特定数据库，登录名必须映射到数据库用户。 数据库内的权限是向数据库用户而不是登录名授予和拒绝授予的。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 需要对数据库拥有 `ALTER ANY USER` 权限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
##### <a name="to-create-a-database-user"></a>创建数据库用户  
  
1.  在对象资源管理器中，展开 **“数据库”** 文件夹。  
  
2.  展开要在其中创建新数据库用户的数据库。  
  
3.  右键单击“安全性”文件夹，指向“新建”，然后选择“用户…”************。  
  
4.  在 "**数据库用户-新建**" 对话框的 "**常规**" 页上，从 "**用户类型**" 列表中选择以下用户类型之一 **：带登录名的 sql 用户**、**没有登录名的 sql**用户、**映射到证书**的用户、映射**到非对称密钥**的用户或**Windows 用户**。  
  
5.  在 **“用户名”** 框中，输入新用户的名称。 如果从 "**用户类型**" 列表中选择了 " **Windows 用户**"，则还可以单击省略号 **（...）** 以打开 "**选择用户或组**" 对话框。  
  
6.  在 **“登录名”** 框中，输入用户的登录名。 或者，单击省略号 (…) 以打开“选择登录名”对话框********。 如果您从 **“用户类型”** 列表中选择了 **“带登录名的 SQL 用户”** 或 **“Windows 用户”** ，则 **“登录名”** 可用。  
  
7.  在 **“默认架构”** 框中，指定此用户所创建的对象所属的架构。 或者，单击省略号 (…) 以打开“选择架构”对话框********。 如果您从 **“用户类型”** 列表中选择了 **“带登录名的 SQL 用户”**, **“不带登录名的 SQL 用户”** 或 **“Windows 用户”** ，则 **“默认架构”** 可用。  
  
8.  在 **“证书名称”** 框中，输入要用于数据库用户的证书。 或者，单击省略号 (…) 以打开“选择证书”对话框********。 如果从 **“用户类型”** 列表中选择了 **“映射到证书的用户”** ，则 **“证书名称”** 可用。  
  
9. 在“非对称密钥名称” ****  框中，输入要用于数据库用户的密钥。 或者，单击省略号 (…) 以打开“选择非对称密钥”对话框********。 如果从 **“用户类型”** 列表中选择了 **“映射到非对称密钥的用户”** ，则 **“非对称密钥名称”** 可用。  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>其他选项  
 “数据库用户 - 新建”**** 对话框还在四个其他页面上提供了选项：“拥有的架构”、“成员身份”、“安全对象”和“扩展属性”****************。  
  
-   **“拥有的架构”** 页列出了可由新的数据库用户拥有的所有可能的架构。 若要向数据库用户添加架构或者从数据库用户中删除架构，请在 **“此用户拥有的架构”** 下选中或取消选中架构旁边的复选框。  
  
-   **“成员身份”** 页列出了可由新的数据库用户拥有的所有可能的数据库成员身份角色。 若要向数据库用户添加角色或者从数据库用户中删除角色，请在 **“数据库角色成员身份”** 下选中或取消选中角色旁边的复选框。  
  
-   **“安全对象”** 页将列出所有可能的安全对象以及可授予登录名的针对这些安全对象的权限。  
  
-   **“扩展属性”** 页允许您向数据库用户添加自定义属性。 此页还提供以下选项：  
  
     **Database**  
     显示所选数据库的名称。 此字段为只读。  
  
     **排序规则**  
     显示用于所选数据库的排序规则。 此字段为只读。  
  
     **属性**  
     查看或指定对象的扩展属性。 每个扩展属性都由与该对象关联的元数据的名称/值对组成。  
  
     **省略号 (...)**  
     单击“值”后面的省略号 (…) 按钮可打开“已扩展属性的值”对话框************。 在这一较大的范围中键入或查看扩展属性的值。 有关详细信息，请参阅 [“扩展属性的值”对话框](../../databases/value-for-extended-property-dialog-box.md)。  
  
     **删除**  
     删除所选扩展属性。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-database-user"></a>创建数据库用户  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```  
    -- Creates the login AbolrousHazem with password '340$Uuxwp7Mcxo7Khy'.  
    CREATE LOGIN AbolrousHazem   
        WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
    GO  
  
    -- Creates a database user for the login created above.  
    CREATE USER AbolrousHazem FOR LOGIN AbolrousHazem;  
    GO  
    ```  
  
 有关详细信息，请参阅 [CREATE USER (Transact-SQL)](/sql/t-sql/statements/create-user-transact-sql)。  
  
## <a name="see-also"></a>另请参阅  
 [主体（数据库引擎）](principals-database-engine.md)  
  
  
