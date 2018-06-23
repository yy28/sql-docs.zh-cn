---
title: 创建 ActiveX 脚本作业步骤 | Microsoft Docs
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
- ActiveX scripting jobs [SQL Server]
- job steps [Analysis Services]
ms.assetid: e6c46c6b-2d61-4571-bc8e-a831cd6e6302
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d8e5ecaa2472dab26cc6be661bea7220748a6a39
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017670"
---
# <a name="create-an-activex-script-job-step"></a>Create an ActiveX Script Job Step
  本主题介绍如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../includes/tsql-md.md)] 或 SQL Server 管理对象，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中创建和定义用于执行 ActiveX 脚本的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业步骤。  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要创建 Transact-SQL 作业步骤，可使用：**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理对象](#SMO)  
  
## <a name="before-you-begin"></a>开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
###  <a name="Security"></a> 安全性  
 有关详细信息，请参阅 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-an-activex-script-job-step"></a>创建 ActiveX 脚本作业步骤  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的实例，然后展开该实例。  
  
2.  展开 **“SQL Server 代理”**，创建一个新作业或右键单击一个现有作业，再单击 **“属性”**。 有关创建作业的详细信息，请参阅 [创建作业](create-jobs.md)。  
  
3.  在 **“作业属性”** 对话框中，单击 **“步骤”** 页，再单击 **“新建”**。  
  
4.  在 **“新建作业步骤”** 对话框中，键入作业的 **“步骤名称”**。  
  
5.  在 **“类型”** 列表中，单击 **“ActiveX 脚本”**。  
  
6.  在 **“运行身份”** 列表中，选择该作业将要使用的代理帐户和凭据。  
  
7.  选择编写脚本的 **“语言”** 。 或者，单击 **“其他”** ，然后输入编写脚本使用的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX 脚本语言。  
  
8.  在 **“命令”** 框中，输入将要对作业步骤执行的脚本语法。 或者，单击 **“打开”** ，选择包含脚本语法的文件。  
  
9. 单击 **“高级”** 页设置以下作业步骤选项：当该作业步骤成功或失败时将执行的操作、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理应该尝试执行该作业步骤的次数以及重试的时间间隔。  
  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-create-an-activex-script-job-step"></a>创建 ActiveX 脚本作业步骤  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
  
              -- create an ActiveX Script job step written in VBScript that creates a restore point  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Create a restore point',  
        @subsystem = N'ACTIVESCRIPTING',  
        @command = N'Const RESTORE_POINT = 20  
  
    strComputer = "."  
    Set objWMIService = GetObject("winmgmts:" _  
        & "{impersonationLevel=impersonate}!\\" & strComputer & "\root\default")  
  
    Set objItem = objWMIService.Get("SystemRestore")  
    errResults = objItem.Restore(RESTORE_POINT)',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
 有关详细信息，请参阅[sp_add_jobstep &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)。  
  
##  <a name="SMO"></a> 使用 SQL Server 管理对象  
 **创建 ActiveX 脚本作业步骤**  
  
 使用`JobStep`通过使用一种选择，如 Visual Basic、 Visual C# 或 PowerShell 编程语言的类。  
  
  
