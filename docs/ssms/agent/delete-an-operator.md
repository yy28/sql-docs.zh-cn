---
title: "删除操作员 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, operators
- canceling operators
- removing operators
- deleting operators
- dropping operators
- jobs [SQL Server Agent], operators
- operators (users) [Database Engine], deleting with Management Studio
ms.assetid: 2b7b8627-082d-4189-8584-abd3a9b604cf
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c2a8e64f1e186be0ff1e9ef82aeb23171bc7b7d0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="delete-an-operator"></a>Delete an Operator
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 本主题介绍了如何通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 或 [!INCLUDE[tsql](../../includes/tsql_md.md)]，在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中删除操作员，使他们不会再收到 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理警报通知。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [限制和局限](#Restrictions)  
  
    [Security](#Security)  
  
-   **若要删除操作员，请使用：**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Restrictions"></a>限制和局限  
删除操作员时，将同时删除与此操作员关联的所有通知。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
**sysadmin** 固定服务器角色的成员可以删除操作员。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-delete-an-operator"></a>删除操作员  
  
1.  在 **“对象资源管理器”**中，单击加号以展开包含要删除的操作员的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  单击加号以展开 **“操作员”** 文件夹。  
  
4.  右键单击要删除的操作员，然后选择“删除”。  
  
5.  在 **“删除对象”** 对话框中，确保已选择正确的操作员，然后单击 **“确定”**。 如果希望其他操作员收到发送给已删除操作员的警报和作业，请选择 **“重新分配给”** ，然后在列表中选择一个操作员。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-delete-an-operator"></a>删除操作员  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    -- deletes operator 'Test Operator' and reassigns all alerts and jobs
    --  sent to that operator to 'François Ajenstat'  
    USE msdb ;  
    GO  
  
    EXEC sp_delete_operator @name = 'Test Operator',  
        @reassign_to_operator = 'François Ajenstat';  
    GO  
    ```  
  
有关详细信息，请参阅 [sp_delete_operator (Transact-SQL)](http://msdn.microsoft.com/en-us/ff6c2c4b-e9fe-4d0c-bbc2-a2ddcc1acb95)。  
  
