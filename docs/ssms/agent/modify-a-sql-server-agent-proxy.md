---
title: "修改 SQL Server 代理程序代理 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- proxies [SQL Server Agent], modifying
- modifying SQL Server Agent proxy
ms.assetid: 6e1dfbaa-8089-4813-940c-d5a2e13d8552
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3380732d0cce979849a41d43567783a6c7df3a71
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="modify-a-sql-server-agent-proxy"></a>Modify a SQL Server Agent Proxy
本主题介绍了如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 或 [!INCLUDE[tsql](../../includes/tsql_md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中修改 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理的代理。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [限制和局限](#Restrictions)  
  
    [Security](#Security)  
  
-   **若要修改 SQL Server 代理的代理帐户，请使用：**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Restrictions"></a>限制和局限  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理的代理帐户使用凭据存储 Windows 用户帐户的相关信息。 凭据中指定的用户必须对正在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 的计算机具有“以批处理作业登录”权限。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理检查代理帐户的子系统访问权限，并在每次运行作业步骤时向代理帐户授予访问权限。 如果代理对子系统不再具有访问权限，则作业步骤将失败。 否则， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理将模拟代理帐户中指定的用户并运行作业步骤。  
  
-   如果用户的登录帐户具有访问代理帐户的权限，或者用户属于具有访问代理帐户的权限的任何角色，则用户可以在作业步骤中使用代理帐户。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
只有 **sysadmin** 固定服务器角色的成员才能创建、修改或删除代理帐户。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-modify-a-includessnoversionincludesssnoversionmdmd-agent-proxy"></a>修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理的代理帐户  
  
1.  在 **“对象资源管理器”**中，单击加号以展开包含要修改的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理的代理帐户的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  单击加号以便展开 **“代理”** 文件夹。  
  
4.  单击加号以展开代理的子系统节点（例如，“ActiveX 脚本”）。  
  
5.  右键单击要修改属性的代理帐户，然后选择“属性”。  
  
6.  在“proxy_name 代理帐户属性”对话框中，根据需要更改代理帐户。 有关此对话框中的选项的详细信息，请参阅[创建 SQL Server 代理的代理](../../ssms/agent/create-a-sql-server-agent-proxy.md)。  
  
7.  完成后，单击 **“确定”**。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-modify-a-includessnoversionincludesssnoversionmdmd-agent-proxy"></a>修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理的代理帐户  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    -- Disables the proxy named 'Catalog application proxy'.  
    USE msdb ;  
    GO  
    EXEC dbo.sp_update_proxy  
        @proxy_name = 'Catalog application proxy',  
        @enabled = 0;  
    GO  
    ```  
  
有关详细信息，请参阅 [sp_update_proxy (Transact-SQL)](http://msdn.microsoft.com/en-us/864fd0e6-9d61-4f07-92ef-145318d2f881)。  
  

