---
title: 从基于策略的管理策略评估该策略 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: 0b3214bd-d0ab-45ab-9281-3d95507abe54
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a1828ceb08481a3d41b05cd6735e6b2741827e6f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130097"
---
# <a name="evaluate-a-policy-based-management-policy-from-that-policy"></a>从基于策略的管理策略评估该策略
  本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中使用策略来评估该策略。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **若要评估某个策略，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 要求具有 msdb 数据库中 PolicyAdministratorRole 角色的成员身份。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-evaluate-a-policy"></a>评估策略  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开包含要评估的策略的服务器。  
  
2.  单击加号以便展开 **“管理”** 文件夹。  
  
3.  单击加号以便展开 **“策略管理”**。  
  
4.  单击加号以便展开 **“策略”** 文件夹。  
  
5.  右键单击要评估的策略，然后选择“评估”。  
  
6.  在 **“评估结果”**  对话框中，可查看策略评估的结果。 对于不符合策略且具有可通过基于策略的管理进行重新配置的属性的目标，可以通过单击“应用”强制符合策略。 有关 **“评估策略** 对话框中的可用选项的详细信息，请参阅 [Evaluate Policies Dialog Box, Policy Selection Page](evaluate-policies-dialog-box-policy-selection-page.md) 和 [Evaluate Policies Dialog Box, Evaluation Results Page](evaluate-policies-dialog-box-evaluation-results-page.md)。  
  
7.  完成后，单击“关闭”。  
  
  