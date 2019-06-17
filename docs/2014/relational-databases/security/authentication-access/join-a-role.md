---
title: 加入角色 | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.DATABASEUSER.MEMBERSHIP.F1
helpviewer_keywords:
- adding a member to a role
- join a role
ms.assetid: 05c8d10d-5823-46c6-8b1a-81722da6a42b
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: d1c846f7ed60bbecac64021e9a881312e1f1f64c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63011346"
---
# <a name="join-a-role"></a>加入角色
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中向登录名和数据库用户分配角色。 可使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的角色高效地管理权限。 将权限分配给角色，然后在角色中添加和删除用户以及登录名。 通过使用角色，不必针对各个用户单独维护权限。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持四种类型的角色。  
  
-   固定服务器角色  
  
-   用户定义的服务器角色  
  
-   固定的数据库角色  
  
-   用户定义的数据库角色  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中会自动提供固定角色。 固定角色具有完成常见任务必需的权限。 有关固定角色的详细信息，请参阅以下链接。 用户定义的角色由您创建，并可使用选择的权限进行自定义。 有关用户定义角色的详细信息，请参阅以下链接。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要向登录名和数据库用户分配角色，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   更改数据库角色的名称不会更改角色的 ID 号、所有者或权限。  
  
-   在 sys.database_role_members 和 sys.database_principals 目录视图中可以查看数据库角色。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要`ALTER ANY ROLE`上，对数据库的权限`ALTER`权限的角色或中的成员身份**db_securityadmin**。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-add-a-member-to-a-fixed-server-role"></a>向固定服务器角色添加成员  
  
1.  在“对象资源管理器”中，展开要在其中编辑固定服务器角色的服务器。  
  
2.  展开 **“安全性”** 文件夹。  
  
3.  展开 **“服务器角色”** 文件夹。  
  
4.  右键单击要编辑的角色，然后选择“属性”  。  
  
5.  在中**服务器角色属性-** _server_role_name_对话框中，在**成员**页上，单击**添加**。  
  
6.  在“选择服务器登录名或角色”  对话框的“输入要选择的对象名称(示例)”  下，输入要添加到该服务器角色的登录名或服务器角色。 或者，单击“浏览...”，然后在“浏览对象”对话框中选择任意对象或所有可用对象   。 单击**确定**回到**服务器角色属性-** _server_role_name_对话框。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-add-a-member-to-a-user-defined-database-role"></a>向用户定义的数据库角色添加成员  
  
1.  在“对象资源管理器”中，展开要在其中编辑用户定义的数据库角色的服务器。  
  
2.  展开 **“数据库”** 文件夹。  
  
3.  展开要在其中编辑用户定义的数据库角色的数据库。  
  
4.  展开 **“安全性”** 文件夹。  
  
5.  展开 **“角色”** 文件夹。  
  
6.  展开 **“服务器角色”** 文件夹。  
  
7.  右键单击要编辑的角色，然后选择“属性”  。  
  
8.  在中**数据库角色属性-** _database_role_name_对话框中，在**常规**页上，单击**添加**。  
  
9. 在“选择数据库用户或角色”  对话框的“输入要选择的对象名称(示例)”  下，输入要添加到该数据库角色的登录名或数据库角色。 或者，单击“浏览...”，然后在“浏览对象”对话框中选择任意对象或所有可用对象   。 单击**确定**回到**数据库角色属性-** _database_role_name_对话框。  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-add-a-member-to-a-fixed-server-role"></a>向固定服务器角色添加成员  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```  
    ALTER SERVER ROLE diskadmin ADD MEMBER [Domain\Juan] ;  
    GO  
    ```  
  
 有关详细信息，请参阅 [ALTER ROLE (Transact-SQL)](/sql/t-sql/statements/alter-role-transact-sql)。  
  
#### <a name="to-add-a-member-to-a-user-defined-database-role"></a>向用户定义的数据库角色添加成员  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```  
    ALTER ROLE Marketing ADD MEMBER [Domain\Juan] ;  
    GO  
    ```  
  
 有关详细信息，请参阅 [sp_addrolemember (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)。  
  
## <a name="see-also"></a>请参阅  
 [服务器级别角色](server-level-roles.md)   
 [数据库级别的角色](../authentication-access/database-level-roles.md)   
 [应用程序角色](../authentication-access/application-roles.md)  
  
  
