---
title: 导入基于策略的管理策略 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, import policy
ms.assetid: 850b7ef9-d2b7-4754-bf04-7cb419ffb776
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 40c9e6e32cebd7811a57ae1b8154fb446d8f90e4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37302307"
---
# <a name="import-a-policy-based-management-policy"></a>导入基于策略的管理策略
  本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中导入基于策略的管理策略实例。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要导入策略实例，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 附带可用于监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的策略。 默认情况下，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]中未安装这些策略；不过，可以从默认安装位置 C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033 导入这些策略。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 要求具有 msdb 数据库中 PolicyAdministratorRole 角色的成员身份。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-import-a-policy-instance"></a>导入策略实例  
  
1.  在“对象资源管理器” 中，单击加号以展开新导入的策略实例要存储到的服务器。  
  
2.  单击加号以便展开 **“管理”** 文件夹。  
  
3.  单击加号以便展开 **“策略管理”**。  
  
4.  右键单击“策略”文件夹，然后选择“导入策略”。  
  
5.  在“导入”对话框中，键入该文件的路径和名称；或者使用“浏览”按钮 (**...**) 查找包含策略的 XML 文件，然后选择该文件。 有关 **“导入”** 对话框中可用选项的详细信息，请参阅 [Import Policies Dialog Box](import-policies-dialog-box.md)。  
  
6.  完成后，单击 **“确定”**。  
  
  
