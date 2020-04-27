---
title: 查看或修改基于策略的管理策略的属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, modify policies
- Policy-Based Management, view policies
ms.assetid: ba805504-5db5-4731-a8da-a0e89cb20c37
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6d5b5b5ee05f467c0881b38108d126da523ea2e7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62676935"
---
# <a name="view-or-modify-the-properties-of-a-policy-based-management-policy"></a>查看或修改基于策略的管理策略的属性
  本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中查看或修改基于策略的管理策略的属性。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要查看或修改策略的属性，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 要求具有 msdb 数据库中 PolicyAdministratorRole 角色的成员身份。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-the-properties-of-all-policies-on-an-object"></a>查看对象的所有策略的属性  
  
1.  在对象资源管理器中，右键单击某个服务器、服务器对象、数据库或数据库对象，指向“策略”****，然后选择“查看”****。 若要深入了解“查看策略 - object_name”对话框中的可用选项息，请参阅[查看策略对话框](view-policies-dialog-box.md)****__。  
  
2.  **** 完成后，单击“关闭”。  
  
#### <a name="to-view-or-modify-a-specific-policys-properties"></a>查看或修改特定策略的属性  
  
1.  在“对象资源管理器”**** 中，单击加号以便展开包含你要查看或修改的基于策略的管理策略的服务器。  
  
2.  单击加号以便展开 **“管理”** 文件夹。  
  
3.  单击加号以便展开 **“策略管理”**。  
  
4.  单击加号以便展开 **“策略”** 文件夹。  
  
5.  右键单击要查看或修改的策略，然后选择“属性”****。 若要深入了解“打开策略 - policy_name”对话框中的可用选项，请参阅[创建新策略或打开策略对话框，“常规”页](../../integration-services/general-page-of-integration-services-designers-options.md)和[创建新策略或打开策略对话框，“说明”页](create-new-policy-or-open-policy-dialog-box-description-page.md)****__。  
  
6.  完成后，单击“确定”****。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-a-policys-properties"></a>查看策略属性  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
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
  
  
