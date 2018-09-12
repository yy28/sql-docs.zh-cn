---
title: 创建 Transact-SQL 作业步骤 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL job step
- job steps [Transact-SQL]
- SQL Server Agent jobs, Transact-SQL step
ms.assetid: 69c571a7-debe-4063-9d38-e4b6a1e8e84c
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 925d8a66a6764f70381e5d22871e1a5b4ef88e68
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43820713"
---
# <a name="create-a-transact-sql-job-step"></a>Create a Transact-SQL Job Step
  本主题介绍如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../includes/tsql-md.md)] 或 SQL Server 管理对象，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中创建用于执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理作业步骤。  
  
 这些作业步骤脚本可以调用存储过程和扩展存储过程。 一个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作业步骤可以包含多个批处理和嵌入的 GO 命令。 有关创建作业的详细信息，请参阅 [创建作业](create-jobs.md)。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **若要创建 Transact-SQL 作业步骤，可使用：**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理对象](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
 有关详细信息，请参阅 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-transact-sql-job-step"></a>创建 Transact-SQL 作业步骤  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的实例，然后展开该实例。  
  
2.  展开 **“SQL Server 代理”**，创建一个新作业或右键单击一个现有作业，再单击 **“属性”**。  
  
3.  在 **“作业属性”** 对话框中，单击 **“步骤”** 页，再单击 **“新建”**。  
  
4.  在 **“新建作业步骤”** 对话框中，键入作业的 **“步骤名称”**。  
  
5.  在“类型”列表中，单击“Transact-SQL 脚本 (TSQL)”。  
  
6.  在 **“命令”** 框中，键入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批命令，或者单击 **“打开”** ，选择一个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 文件用作命令。  
  
7.  单击 **“分析”** 检查语法。  
  
8.  如果语法正确，将显示“分析成功”消息。 如果发现错误，更正语法后再继续。  
  
9. 单击 **“高级”** 页设置以下作业步骤选项，例如：当该作业步骤成功或失败时将执行的操作、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理应该尝试执行该作业步骤的次数，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理将作业步骤输出写入哪个文件或表。 只有 **sysadmin** 固定服务器角色的成员才可以将作业步骤输出写入到操作系统文件中。 所有 SQL Server 代理用户都可以将输出写入表中。  
  
10. 如果您是 **sysadmin** 固定服务器角色的成员，并且希望以其他 SQL 登录身份运行此作业步骤，请从 **“作为以下用户运行”** 列表中选择 SQL 登录名。  
  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-transact-sql-job-step"></a>创建 Transact-SQL 作业步骤  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    -- creates a job step that that uses Transact-SQL  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
 有关详细信息，请参阅[sp_add_jobstep &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)。  
  
##  <a name="SMO"></a> 使用 SQL Server 管理对象  
 **创建 Transact-SQL 作业步骤**  
  
 使用`JobStep`类通过使用一种编程语言的选择，如 Visual Basic、 Visual C# 或 PowerShell。  
  
  
