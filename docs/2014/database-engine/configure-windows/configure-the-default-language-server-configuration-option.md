---
title: 配置“默认语言”服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- default language option
ms.assetid: c08c26d8-5a62-487e-a4ee-4c529e4f9287
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2ca958583cbdf6fec00d5d507051f10be503abf4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079737"
---
# <a name="configure-the-default-language-server-configuration-option"></a>配置默认语言服务器配置选项
  本主题说明了如何使用 **或** 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中配置 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] “默认语言” [!INCLUDE[tsql](../../includes/tsql-md.md)]服务器配置选项。 **“默认语言”** 选项指定所有新创建的登录名的默认语言。 若要设置默认语言，请指定所需语言的 **langid** 值。 可通过查询 **sys.syslanguages** 兼容性视图来获取 **langid** 值。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [建议](#Recommendations)  
  
     [Security](#Security)  
  
-   **要配置默认语言选项，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **跟进：**  [在配置默认语言选项之后](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Recommendations"></a> 建议  
  
-   可以使用 CREATE LOGIN 或 ALTER LOGIN 替代登录的默认语言。 会话的默认语言是该会话登录的语言，除非使用开放式数据库连接 (ODBC) 或 OLE DB API 替代每个会话的默认语言。 请注意，只能将“默认语言”选项设置为 [sys.syslanguages](/sql/relational-databases/system-compatibility-views/sys-syslanguages-transact-sql) 中定义的语言 ID (0-32)。 在使用包含数据库时，可使用 CREATE DATABASE 或 ALTER DATABASE 设置数据库的默认语言，使用 CREATE USER 或 ALTER USER 设置包含数据库用户的默认语言。 在包含数据库中设置默认语言时，接受 **sys.syslanguages** 中所列的 **langid**值、语言名称或语言别名。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 默认情况下，所有用户都具备不带参数或仅带第一个参数的 **sp_configure** 的执行权限。 若要执行带两个参数的 **sp_configure** 以更改配置选项或运行 RECONFIGURE 语句，则用户必须具备 ALTER SETTINGS 服务器级别的权限。 ALTER SETTINGS 权限由 **sysadmin** 和 **serveradmin** 固定服务器角色隐式持有。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-default-language-option"></a>配置默认语言选项  
  
1.  在对象资源管理器中，右键单击服务器并选择 **“属性”**。  
  
2.  单击 **“杂项服务器设置”** 节点。  
  
3.  在 **“用户的默认语言”** 框中，选择 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 显示系统消息所用的语言。  
  
     默认语言为英语。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-default-language-option"></a>配置默认语言选项  
  
1.  连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例说明如何使用 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 将 `default language` 选项配置为 French (`2`)。  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'default language', 2 ;  
GO  
RECONFIGURE ;  
GO  
```  
  
 有关详细信息，请参阅 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)版本的组合自动配置的最大工作线程数。  
  
##  <a name="FollowUp"></a> 跟进：在配置默认语言选项之后  
 该设置将立即生效，无需重新启动服务器。  
  
## <a name="see-also"></a>请参阅  
 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)   
 [CREATE USER (Transact-SQL)](/sql/t-sql/statements/create-user-transact-sql)   
 [ALTER USER (Transact-SQL)](/sql/t-sql/statements/alter-user-transact-sql)   
 [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)   
 [RECONFIGURE (Transact-SQL)](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
