---
title: 查看 SQL Server 对象的基于策略的管理方面 | Microsoft Docs
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
- Policy-Based Management, view facets
ms.assetid: 5f423b9f-a6c4-41a7-9d8d-8f4926ce1fb4
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e95abe9e853c0e90bed9d58765fae1640f9885f8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015683"
---
# <a name="view-the-policy-based-management-facets-on-a-sql-server-object"></a>查看 SQL Server 对象的基于策略的管理方面
  本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中查看应用到特定 SQL Server 对象的所有基于策略的管理方面。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **若要查看对象的所有方面，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 要求具有 msdb 数据库中 PolicyAdministratorRole 角色的成员身份。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-all-of-the-facets-in-an-object"></a>查看对象的所有方面  
  
1.  在对象资源管理器中，右键单击 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例、实例对象、数据库或数据库对象，然后单击“Facet”。  
  
2.  在“查看 Facet – object_name”对话框的“Facet”列表中，选择某一 Facet，查看其属性。 有关此对话框上可用选项的详细信息，请参阅 [View Facets Dialog Box](view-facets-dialog-box.md)。  
  
3.  完成后，单击 **“确定”**。  
  
  