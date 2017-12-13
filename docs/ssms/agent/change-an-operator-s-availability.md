---
title: "更改操作员的可用性 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
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
- reactivating operators
- removing operators
- deleting operators
- available operators [SQL Server]
- dropping operators
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
- disabling operators
- operators (users) [Database Engine], changing availability with Management Studio
ms.assetid: 10d58b92-b67b-47e2-af9c-9f9fd6968bba
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aef98b74c420cc0f4edc8f4b041db385c6163e70
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="change-an-operator39s-availability"></a>更改操作员的可用性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 本主题介绍了如何通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 或 [!INCLUDE[tsql](../../includes/tsql_md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中更改操作员接收警报通知的计划。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [Security](#Security)  
  
-   **若要更改操作员的可用性，请使用：**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
只有 **sysadmin** 固定服务器角色的成员才能编辑操作员。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-change-an-operators-availability"></a>更改操作员的可用性  
  
1.  在 **“对象资源管理器”**中，单击加号以展开包含要启用或禁用的操作员的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  单击加号以展开 **“操作员”** 文件夹。  
  
4.  右键单击要启用或禁用的操作员，选择“属性”，然后单击“常规”选项卡。  
  
5.  在“operator_name 属性”对话框中，选中或清除“启用”复选框。  
  
6.  单击 **“确定”**。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-change-an-operators-availability"></a>更改操作员的可用性  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    -- disables the 'François Ajenstat' operator  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_operator   
        @name = N'François Ajenstat',  
        @enabled = 0;  
    GO  
    ```  
  
有关详细信息，请参阅 [sp_update_operator (Transact-SQL)](http://msdn.microsoft.com/en-us/231750a6-4828-4d03-afe6-b91d38c42ed3)。  
  
