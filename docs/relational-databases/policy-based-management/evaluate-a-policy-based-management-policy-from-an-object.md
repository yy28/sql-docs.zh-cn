---
title: "评估来自对象的基于策略的管理策略 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "基于策略的管理, 评估策略"
ms.assetid: b9e9d646-4894-4dee-a02a-0c71a8dc020e
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 8
---
# 评估来自对象的基于策略的管理策略
  本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中评估来自服务器实例、数据库或数据库对象的策略。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要从对象评估策略，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   执行模式定义为策略的一部分，无法在 **“评估策略”** 对话框中更改。  
  
-   **“评估策略”** 对话框仅显示适用于数据库对象的策略。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 要求具有 msdb 数据库中 PolicyAdministratorRole 角色的成员身份。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 从对象评估策略  
  
1.  在对象资源管理器中，右键单击某个服务器实例、数据库或数据库对象，指向“策略”，然后选择“评估”。  
  
2.  在 **“评估策略”** 对话框中，选择一个或多个策略，然后单击 **“评估”** 以在评估模式下运行策略。 这会为目标集生成符合报告，但不会重新配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或强制要求以后符合策略。 对于不符合所选策略且具有可通过基于策略的管理进行重新配置的属性的目标，可以通过单击“应用”强制符合策略。 有关 **“评估策略** 对话框中的可用选项的详细信息，请参阅 [Evaluate Policies Dialog Box, Policy Selection Page](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-policy-selection-page.md)、 [Evaluate Policies Dialog Box, Evaluation Results Page](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-evaluation-results-page.md)和 [Results Detailed View Dialog Box](../../relational-databases/policy-based-management/results-detailed-view-dialog-box.md)。  
  
3.  完成后，单击 **“关闭”**。  
  
  