---
title: "查看或修改基于策略的管理策略的属性 | Microsoft Docs"
ms.custom: 
ms.date: 10/06/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, modify policies
- Policy-Based Management, view policies
ms.assetid: ba805504-5db5-4731-a8da-a0e89cb20c37
caps.latest.revision: "9"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7bfecfe67bf04c5145c600ce1ce59546aecec73b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="view-or-modify-the-properties-of-a-policy-based-management-policy"></a>查看或修改基于策略的管理策略的属性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]本主题介绍如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中查看或修改基于策略的管理策略的属性。  
  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
  
####  <a name="Permissions"></a> Permissions  
 要求具有 msdb 数据库中 PolicyAdministratorRole 角色的成员身份。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-the-properties-of-all-policies-on-an-object"></a>查看对象的所有策略的属性  
  
1.  在对象资源管理器中，右键单击某个服务器、服务器对象、数据库或数据库对象，指向“策略”，然后选择“查看”。 有关“查看策略 – *object_name*”对话框中的可用选项的详细信息，请参阅[“查看策略”对话框](../../relational-databases/policy-based-management/view-policies-dialog-box.md)。  
  
2.  完成后，单击“关闭”。  
  
#### <a name="to-view-or-modify-a-specific-policys-properties"></a>查看或修改特定策略的属性  
  
1.  在“对象资源管理器”中，单击加号以便展开包含你要查看或修改的基于策略的管理策略的服务器。  
  
2.  单击加号以便展开 **“管理”** 文件夹。  
  
3.  单击加号以便展开 **“策略管理”**。  
  
4.  单击加号以便展开 **“策略”** 文件夹。  
  
5.  右键单击要查看或修改的策略，然后选择“属性”。 有关“打开策略 - *policy_name*”对话框中的可用选项的详细信息，请参阅[“创建新策略”或“打开策略”对话框，“常规”页](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-general-page.md)和[“创建新策略”或“打开策略”对话框，“说明”页](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-description-page.md)。  
  
6.  完成后，单击 **“确定”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-a-policys-properties"></a>查看策略属性  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
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
  
 有关详细信息，请参阅 [syspolicy_policies (Transact-SQL)](../../relational-databases/system-catalog-views/syspolicy-policies-transact-sql.md)。  
  
  
