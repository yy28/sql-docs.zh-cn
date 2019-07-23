---
title: 创建 SQL Server 代理程序代理 | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- proxies [SQL Server Agent], creating
ms.assetid: 142e0c55-a8b9-4669-be49-b9dc602d5988
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1ba8bbd7b78a2ca0a246bf01836a33f2592a8c82
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68251719"
---
# <a name="create-a-sql-server-agent-proxy"></a>创建 SQL Server 代理的代理帐户
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中创建 SQL Server 代理的代理。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的代理帐户定义作业步骤可以运行的安全上下文。 每个代理对应于一个安全凭据。 若要设置特定作业步骤的权限，请创建一个具有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理子系统所需权限的代理，再将该代理分配给该作业步骤。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [限制和局限](#Restrictions)  
  
    [安全性](#Security)  
  
-   **若要创建 SQL Server 代理的代理帐户，请使用：**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Restrictions"></a>限制和局限  
  
-   如果没有凭据，那么在创建代理之前必须先创建凭据。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的代理帐户使用凭据存储 Windows 用户帐户的相关信息。 凭据中指定的用户必须对运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机具有“从网络访问此计算机”权限 (SeNetworkLogonRight)。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理检查代理帐户的子系统访问权限，并在每次运行作业步骤时向代理帐户授予访问权限。 如果代理对子系统不再具有访问权限，则作业步骤将失败。 否则，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理将模拟代理帐户中指定的用户并运行作业步骤。  
  
-   创建代理帐户不会更改凭据中指定的用户对代理帐户具有的权限。 例如，您可以为不具有连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的权限的用户创建代理帐户。 在这种情况下，使用该代理帐户的作业步骤无法连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   如果用户的登录帐户具有访问代理帐户的权限，或者用户属于具有访问代理帐户的权限的任何角色，则用户可以在作业步骤中使用代理帐户。  
  
### <a name="Security"></a>安全性  
  
#### <a name="Permissions"></a>Permissions  
  
-   只有 **sysadmin** 固定服务器角色的成员才有权创建、修改或删除代理帐户。 必须将不属于 sysadmin 固定服务器角色成员的用户添加到 msdb 数据库中的以下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理固定数据库角色之一，才能使用代理   ：SQLAgentUserRole、SQLAgentReaderRole 或 SQLAgentOperatorRole    。  
  
-   如果除了代理之外还需要创建凭据，则需要 **ALTER ANY CREDENTIAL** 权限。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-create-a-sql-server-agent-proxy"></a>创建 SQL Server 代理的代理帐户  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开要在 SQL Server 代理上创建代理的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”** 。  
  
3.  右键单击“代理”  文件夹，然后选择“新建代理”  。  
  
4.  在 **“新建代理帐户”** 对话框的 **“常规”** 页中，在 **“代理名称”** 框中输入代理帐户的名称。  
  
5.  在 **“凭据名称”** 框中，输入代理帐户将使用的安全凭据的名称。  
  
6.  在 **“说明”** 框中输入对代理帐户的说明。  
  
7.  在 **“对以下子系统有效”** 之下，为此代理选择适当的子系统。  
  
8.  在 **“主体”** 页上，添加或删除登录名或角色，以授予或删除对代理帐户的访问权限。  
  
9. 完成后，单击 **“确定”** 。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-create-a-sql-server-agent-proxy"></a>创建 SQL Server 代理的代理帐户  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```  
    -- creates credential CatalogApplicationCredential  
    USE msdb ;  
    GO  
    CREATE CREDENTIAL CatalogApplicationCredential WITH IDENTITY = 'REDMOND/TestUser',   
        SECRET = 'G3$1o)lkJ8HNd!';  
    GO  
    -- creates proxy "Catalog application proxy" and assigns
    -- the credential 'CatalogApplicationCredential' to it.  
    EXEC dbo.sp_add_proxy  
        @proxy_name = 'Catalog application proxy',  
        @enabled = 1,  
        @description = 'Maintenance tasks on catalog application.',  
        @credential_name = 'CatalogApplicationCredential' ;  
    GO  
    -- grants the proxy "Catalog application proxy" access to 
    -- the ActiveX Scripting subsystem.  
    EXEC dbo.sp_grant_proxy_to_subsystem  
        @proxy_name = N'Catalog application proxy',  
        @subsystem_id = 2 ;  
    GO  
    ```  
  
有关详细信息，请参阅：  
  
-   [CREATE CREDENTIAL (Transact-SQL)](https://msdn.microsoft.com/d5e9ae69-41d9-4e46-b13d-404b88a32d9d)  
  
-   [sp_add_proxy (Transact-SQL)](https://msdn.microsoft.com/cb59df37-f103-439b-bec1-2871fb669a8b)  
  
-   [sp_grant_proxy_to_subsystem (Transact-SQL)](https://msdn.microsoft.com/866aaa27-a1e0-453a-9b1b-af39431ad9c2)  
  
