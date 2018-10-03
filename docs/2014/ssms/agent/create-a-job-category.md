---
title: 创建作业类别 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
ms.assetid: e24a6d38-d231-4f64-ab89-2d1ef6f5792c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2a2c9966dfbb270165ea5245fd59e0793d165bdb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48127457"
---
# <a name="create-a-job-category"></a>创建作业类别
  本主题介绍如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 管理对象在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中创建作业类别。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理提供了内置作业类别，可以向这些类别分配作业，也可以创建作业类别并对其分配作业。 作业类别有助于您组织作业，从而更容易筛选和分组。 例如，可以将所有数据库备份作业组织到“数据库维护”类别中。 此外，还可以创建自己的作业类别。  
  
 
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
 多服务器类别仅存在于主服务器上。 主服务器上仅提供了一个默认作业类别：“[未分类(多服务器)]”。 下载多服务器作业后，其类别将在目标服务器上更改为“来自 MSX 的作业”  。  
  
###  <a name="Security"></a> 安全性  
 有关详细信息，请参阅 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)。  
  

  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-job-category"></a>创建作业类别  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开您想要在其中创建作业类别的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  右键单击 **“作业”** 文件夹，然后选择 **“管理作业类别”**。  
  
4.  在“管理作业类别server_name” 对话框中，单击“添加”。  
  
5.  在新对话框的 **“名称”** 框中，输入新作业类别的名称。  
  
6.  选中 **“显示所有作业”** 复选框。 通过选中作业对应的框来为新类别选择一个或多个作业。  
  
7.  单击“确定” 。  
  
8.  在“管理作业类别server_name” 对话框中，单击“刷新”，确保新的作业类别处于活动状态。 如果一切都与预期情况相同，则关闭此对话框。  
  
 有关这些对话框的详细信息，请参阅[作业类别： 管理作业类别](job-categories-manage-job-categories.md)并[作业类别属性和新的作业类别](job-categories-properties-new-job-category.md)。  
  
 
  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-job-category"></a>创建作业类别  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    -- creates a local job category named AdminJobs   
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_category  
        @class=N'JOB',  
        @type=N'LOCAL',  
        @name=N'AdminJobs' ;  
    GO  
    ```  
  
 有关详细信息，请参阅[sp_add_category &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-category-transact-sql)。  
  

  
##  <a name="SMO"></a> 使用 SQL Server 管理对象  
 **创建作业类别**  
  
 调用`JobCategory`类通过使用一种编程语言的选择，如 Visual Basic、 Visual C# 或 PowerShell。 有关示例代码，请参阅 [在 SQL Server 代理中计划自动管理任务](sql-server-agent.md)。  
  
 
  
  
