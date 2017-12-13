---
title: "查看有关警报的信息 | Microsoft Docs"
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
- SQL Server Agent, alerts
- viewing alerts
- alerts [SQL Server], viewing
- displaying alerts
- status information [SQL Server], alerts
ms.assetid: a0e3a8c4-e3c2-42a5-b2f8-aa06061d3fa6
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ad441fc481a5dc8fa7efe7d1382fdfc09e5e15e1
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="view-information-about-an-alert"></a>View Information About an Alert
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 本主题说明如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 或 [!INCLUDE[tsql](../../includes/tsql_md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中查看有关 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理警报的信息。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [Security](#Security)  
  
-   **若要查看有关警报的信息，可使用：**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
默认情况下，只有 **sysadmin** 固定服务器角色的成员才能查看有关警报的信息。 其他用户必须被授予 **msdb** 数据库中的 **SQLAgentOperatorRole** 固定数据库角色的权限。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-view-information-about-an-alert"></a>查看有关警报的信息  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开要在其中查看有关警报的信息的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  单击加号以展开 **“警报”** 文件夹。  
  
4.  右键单击包含要查看的信息的警报，然后选择“属性”。  
  
    有关 alert_name“警报属性”对话框中包含的可用选项的详细信息，请参阅：  
  
    -   [警报属性 - 新建警报（“常规”页）](../../ssms/agent/alert-properties-new-alert-general-page.md)  
  
    -   [警报属性 - 新建警报（“响应”页）](../../ssms/agent/alert-properties-new-alert-response-page.md)  
  
    -   [警报属性 - 新建警报（“选项”页）](../../ssms/agent/alert-properties-new-alert-options-page.md)  
  
    -   [警报属性（“历史记录”页）](../../ssms/agent/alert-properties-history-page.md)  
  
5.  完成后，单击 **“确定”**。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-view-information-about-an-alert"></a>查看有关警报的信息  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    -- reports information about the Demo: Sev. 25 Errors alert  
    -- This example assumes that the 'Demo: Sev. 25 Errors' alert exists.  
    USE msdb ;  
    GO  
  
    EXEC sp_help_alert @alert_name = 'Demo: Sev. 25 Errors'  
    GO  
    ```  
  
有关详细信息，请参阅 [sp_help_alert (Transact-SQL)](http://msdn.microsoft.com/en-us/850cef4e-6348-4439-8e79-fd1bca712091)。  
  
