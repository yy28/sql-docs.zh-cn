---
title: 导出基于策略的管理策略 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, export policy
ms.assetid: f0001b33-9078-4432-8460-496736fb325a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0848c4f1a1537eff25db4eabe3de59e890c78f98
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47684922"
---
# <a name="export-a-policy-based-management-policy"></a>导出基于策略的管理策略
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中导出基于策略的管理策略。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **若要导出策略，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 要求具有 msdb 数据库中 PolicyAdministratorRole 角色的成员身份。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-export-a-policy"></a>导出策略  
  
1.  在对象资源管理器中，单击加号以便展开包含您要导出的基于策略的管理策略的服务器。  
  
2.  单击加号以便展开 **“管理”** 文件夹。  
  
3.  单击加号以便展开 **“策略管理”**。  
  
4.  单击加号以便展开 **“策略”** 文件夹。  
  
5.  右键单击要导出的策略，然后选择“导出策略”。  
  
6.  在 **“导出策略”** 对话框中，在地址栏中键入文件的路径和名称。 或者，在对话框的导航窗格中找到文件的合适位置，然后在 **“文件名”** 框中键入 XML 文件的名称。  
  
7.  完成后，单击 **“保存”**。  
  
  
