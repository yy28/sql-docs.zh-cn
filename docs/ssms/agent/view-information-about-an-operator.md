---
title: "查看有关操作员的信息 | Microsoft Docs"
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
- SQL Server Agent jobs, operators
- viewing operators
- operators (users) [Database Engine], viewing with Management Studio
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
- displaying operators
ms.assetid: 92c82cdf-f704-444e-9539-82aea7fe6fb7
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a747402098366d0bbe387b76938fc5fbde8ed87a
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="view-information-about-an-operator"></a>View Information About an Operator
本主题说明如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 或 [!INCLUDE[tsql](../../includes/tsql_md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中查看有关 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理操作员的信息。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [Security](#Security)  
  
-   **若要查看有关操作员的信息，可使用：**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
默认情况下，只有 **sysadmin** 固定服务器角色的成员才可以执行此存储过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-view-information-about-an-operator"></a>查看有关操作员的信息  
  
1.  在 **“对象资源管理器”**中，单击加号以展开包含要查看的操作员的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  单击加号以展开 **“操作员”** 文件夹。  
  
4.  右键单击要查看的操作员，然后选择“属性”。  
  
    有关“operator_name 属性”对话框包含的可用选项的详细信息，请参阅：  
  
    -   [操作员属性 - 新建操作员（“常规”页）](../../ssms/agent/operator-properties-new-operator-general-page.md)  
  
    -   [操作员属性 - 新建操作员（“通知”页）](../../ssms/agent/operator-properties-new-operator-notifications-page.md)  
  
    -   [操作员属性（“历史记录”页）](../../ssms/agent/operator-properties-history-page.md)  
  
5.  完成后，单击 **“确定”**。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-view-information-about-an-operator"></a>查看有关操作员的信息  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    -- reports information about operator François Ajenstat   
    -- This example assumes that the operator exists.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_operator  
        @operator_name = N'François Ajenstat' ;  
    GO  
    ```  
  
有关详细信息，请参阅 [sp_help_operator (Transact-SQL)](http://msdn.microsoft.com/en-us/caedc43d-44b8-415a-897e-92923f6de3b8)。  
  

