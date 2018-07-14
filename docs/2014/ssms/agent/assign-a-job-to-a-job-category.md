---
title: 将作业分配到作业类别 | Microsoft Docs
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
- jobs [SQL Server Agent], assigning
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- SQL Server Agent jobs, assigning
- assigning job to category
ms.assetid: a9ea65a2-1d73-4582-a335-63adeb450cb6
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8dbed6c673968c46264487ed606e2fc2586dd4a6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37275683"
---
# <a name="assign-a-job-to-a-job-category"></a>将作业分配到作业类别
  本主题说明如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../includes/tsql-md.md)] 或 SQL Server 管理对象在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中将 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业分配到作业类别中。  
  
 作业类别有助于您组织作业，从而更容易筛选和分组。 例如，可以将所有数据库备份作业组织到“数据库维护”类别中。 可以将作业分配到内置作业类别，也可以创建用户定义的作业类别，然后将作业分配至其中。  
  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
 有关详细信息，请参阅 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)。  
  
  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-assign-a-job-to-a-job-category"></a>将作业分配到作业类别  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开要将作业分配到作业类别的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  单击加号以便展开 **“作业”** 文件夹。  
  
4.  右键单击要编辑的作业，然后选择“属性”。  
  
5.  在“作业属性 - job_name”对话框的“类别”列表中，选择要分配给作业的作业类别。  
  
6.  单击“确定” 。  
  
  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-assign-a-job-to-a-job-category"></a>将作业分配到作业类别  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    -- adding a new job category to the "NightlyBackups" job  
    USE msdb ;  
    GO  
    EXEC dbo.sp_update_job  
        @job_name = N'NightlyBackups',  
        @category_name = N'[Uncategorized (Local)]';  
    GO  
    ```  
  
 有关详细信息，请参阅[sp_update_job &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql)。  
  
  
  
##  <a name="SMO"></a> 使用 SQL Server 管理对象  
 **将作业分配到作业类别**  
  
 使用`JobCategory`类通过使用一种编程语言的选择，如 Visual Basic、 Visual C# 或 PowerShell。  
  
  
  
  
