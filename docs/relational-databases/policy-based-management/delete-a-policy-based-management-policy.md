---
title: "删除基于策略的管理策略 | Microsoft Docs"
ms.custom: ""
ms.date: "08/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "基于策略的管理, 删除策略"
ms.assetid: 488f0305-190c-4223-aa5c-e9bd43b520eb
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 8
---
# 删除基于策略的管理策略
  本主题介绍如何通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中删除基于策略的管理策略。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要删除策略，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 要求具有 msdb 数据库中 PolicyAdministratorRole 角色的成员身份。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 删除策略  
  
1.  在对象资源管理器中，单击加号以便展开包含您要删除的基于策略的管理策略的服务器。  
  
2.  单击加号以便展开 **“管理”** 文件夹。  
  
3.  单击加号以便展开 **“策略管理”**。  
  
4.  单击加号以便展开 **“策略”** 文件夹。  
  
5.  右键单击要删除的策略，然后选择“删除”。  
  
6.  在 **“删除对象”** 对话框中，确保已选择正确的条件，然后单击 **“确定”**。  
  
  