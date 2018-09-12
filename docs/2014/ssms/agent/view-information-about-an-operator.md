---
title: 查看有关操作员的信息 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- viewing operators
- operators (users) [Database Engine], viewing with Management Studio
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
- displaying operators
ms.assetid: 92c82cdf-f704-444e-9539-82aea7fe6fb7
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 09d7ca532ffd491dc0a79c7c2fe2b97d1120660e
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43809153"
---
# <a name="view-information-about-an-operator"></a>View Information About an Operator
  本主题说明如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中查看有关 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理操作员的信息。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **若要查看有关操作员的信息，可使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才可以执行此存储过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](sql-server-agent-fixed-database-roles.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-information-about-an-operator"></a>查看有关操作员的信息  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开包含要查看的操作员的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  单击加号以展开 **“操作员”** 文件夹。  
  
4.  右键单击要查看的操作员，然后选择“属性”。  
  
     若要深入了解“operator_name属性”对话框包含的可用选项，请参阅：  
  
    -   [操作员属性和新运算符&#40;常规页&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
    -   [运算符属性： 新建操作员&#40;通知页&#41;](operator-properties-new-operator-notifications-page.md)  
  
    -   [操作员属性（“历史记录”页）](operator-properties-history-page.md)  
  
5.  完成后，单击 **“确定”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-information-about-an-operator"></a>查看有关操作员的信息  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    -- reports information about operator François Ajenstat   
    -- This example assumes that the operator exists.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_operator  
        @operator_name = N'François Ajenstat' ;  
    GO  
    ```  
  
 有关详细信息，请参阅[sp_help_operator &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-operator-transact-sql)。  
  
  
