---
title: 查看有关警报的信息 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- viewing alerts
- alerts [SQL Server], viewing
- displaying alerts
- status information [SQL Server], alerts
ms.assetid: a0e3a8c4-e3c2-42a5-b2f8-aa06061d3fa6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c5567abc0893bd183c2468f82278a014e2005113
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211293"
---
# <a name="view-information-about-an-alert"></a>View Information About an Alert
  本主题说明如何使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或[!INCLUDE[tsql](../../includes/tsql-md.md)]在中查看有关代理警报的信息。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要查看有关警报的信息，可使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才能查看有关警报的信息。 其他用户必须被授予 **msdb** 数据库中的 **SQLAgentOperatorRole** 固定数据库角色的权限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-information-about-an-alert"></a>查看有关警报的信息  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开要在其中查看有关警报的信息的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  单击加号以展开 **“警报”** 文件夹。  
  
4.  右键单击包含要查看的信息的警报，然后选择“属性”****。  
  
     有关 alert_name__“警报属性”**** 对话框中包含的可用选项的详细信息，请参阅：  
  
    -   [警报属性-新建警报 &#40;常规页&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
    -   [警报属性-新建警报 &#40;响应 "页面&#41;](alert-properties-new-alert-response-page.md)  
  
    -   [警报属性： "新建警报 &#40;选项" 页面&#41;](alert-properties-new-alert-options-page.md)  
  
    -   [警报属性（“历史记录”页）](alert-properties-history-page.md)  
  
5.  完成后，单击“确定”****。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-information-about-an-alert"></a>查看有关警报的信息  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```  
    -- reports information about the Demo: Sev. 25 Errors alert  
    -- This example assumes that the 'Demo: Sev. 25 Errors' alert exists.  
    USE msdb ;  
    GO  
  
    EXEC sp_help_alert @alert_name = 'Demo: Sev. 25 Errors'  
    GO  
    ```  
  
 有关详细信息，请参阅[&#40;transact-sql&#41;sp_help_alert ](/sql/relational-databases/system-stored-procedures/sp-help-alert-transact-sql)。  
  
  
