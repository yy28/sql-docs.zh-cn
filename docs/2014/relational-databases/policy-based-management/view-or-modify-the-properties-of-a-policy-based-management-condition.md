---
title: 查看或修改基于策略的管理条件的属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view policy conditions
- Policy-Based Management, modify policy conditions
ms.assetid: 890d7384-8444-4767-bb6f-f5debb155747
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 340423e23037ae401b1e5749fbed38b1822cfb41
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62677013"
---
# <a name="view-or-modify-the-properties-of-a-policy-based-management-condition"></a>查看或修改基于策略的管理条件的属性
  本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中查看或修改基于策略的管理条件的属性。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要查看或修改条件的属性，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 要求具有 msdb 数据库中 PolicyAdministratorRole 角色的成员身份。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-or-modify-a-conditions-properties"></a>查看或修改条件的属性  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开包含要查看或修改的条件的服务器。  
  
2.  单击加号以便展开 **“管理”** 文件夹。  
  
3.  单击加号以便展开 **“策略管理”** 。  
  
4.  单击加号以便展开 **“条件”** 文件夹。  
  
5.  右键单击要查看或编辑的条件，然后选择“属性”  。 若要深入了解“打开条件 - condition_name”对话框中的可用选项，请参阅[“创建新条件”或“打开条件”对话框，“常规”页](../../integration-services/general-page-of-integration-services-designers-options.md)、[“打开条件”对话框，“依赖策略”页](open-condition-dialog-box-dependent-policies-page.md)、[“创建新条件”或“打开条件”对话框，“说明”页](create-new-condition-or-open-condition-dialog-box-description-page.md)和[“高级编辑”（条件）对话框](advanced-edit-condition-dialog-box.md)   。  
  
6.  完成后，单击 **“确定”** 。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-a-conditions-properties"></a>查看条件的属性  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```  
    USE msdb;  
    GO  
    SELECT name,  
       description,  
       facet,  
       expression,  
       is_name_condition,  
       obj_name  
    FROM syspolicy_conditions;  
    GO  
  
    ```  
  
 有关详细信息，请参阅 [syspolicy_conditions (Transact-SQL)](/sql/relational-databases/system-catalog-views/syspolicy-conditions-transact-sql)。  
  
  
