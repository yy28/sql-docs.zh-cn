---
title: 查看或修改基于策略的管理策略的属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, modify policies
- Policy-Based Management, view policies
ms.assetid: ba805504-5db5-4731-a8da-a0e89cb20c37
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fa2e53e51bc45f1bf3f00d3ac82c499e724c66a8
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43815963"
---
# <a name="view-or-modify-the-properties-of-a-policy-based-management-policy"></a>查看或修改基于策略的管理策略的属性
  本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中查看或修改基于策略的管理策略的属性。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **若要查看或修改策略的属性，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 要求具有 msdb 数据库中 PolicyAdministratorRole 角色的成员身份。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-the-properties-of-all-policies-on-an-object"></a>查看对象的所有策略的属性  
  
1.  在对象资源管理器中，右键单击某个服务器、服务器对象、数据库或数据库对象，指向“策略”，然后选择“查看”。 若要深入了解“查看策略 – object_name”对话框中的可用选项息，请参阅[“查看策略”对话框](view-policies-dialog-box.md)。  
  
2.  完成后，单击“关闭”。  
  
#### <a name="to-view-or-modify-a-specific-policys-properties"></a>查看或修改特定策略的属性  
  
1.  在“对象资源管理器”中，单击加号以便展开包含你要查看或修改的基于策略的管理策略的服务器。  
  
2.  单击加号以便展开 **“管理”** 文件夹。  
  
3.  单击加号以便展开 **“策略管理”**。  
  
4.  单击加号以便展开 **“策略”** 文件夹。  
  
5.  右键单击要查看或修改的策略，然后选择“属性”。 若要深入了解“打开策略 - policy_name”对话框中的可用选项，请参阅[“创建新策略”或“打开策略”对话框，“常规”页](../../integration-services/general-page-of-integration-services-designers-options.md)和[“创建新策略”或“打开策略”对话框，“说明”页](create-new-policy-or-open-policy-dialog-box-description-page.md)。  
  
6.  完成后，单击 **“确定”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-a-policys-properties"></a>查看策略属性  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    USE msdb;  
    GO  
    SELECT name,  
       execution_mode,  
       description,  
       is_enabled,  
       job_id  
    FROM syspolicy_policies;  
    GO  
    ```  
  
 有关详细信息，请参阅 [syspolicy_policies (Transact-SQL)](/sql/relational-databases/system-catalog-views/syspolicy-policies-transact-sql)。  
  
  
