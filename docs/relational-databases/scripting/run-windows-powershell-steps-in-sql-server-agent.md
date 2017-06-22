---
title: "在 SQL Server 代理中运行 Windows PowerShell 步骤 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f25f7549-c9b3-4618-85f2-c9a08adbe0e3
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ae35fb3deecc8b77940ab76d1b0f016f00f39e27
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="run-windows-powershell-steps-in-sql-server-agent"></a>在 SQL Server 代理中运行 Windows PowerShell 步骤
  使用 SQL Server 代理可以在计划时间运行 SQL Server PowerShell 脚本。  
  
1.  **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions)  
  
2.  **To run PowerShell from SQL Server Agent, using:**  [PowerShell Job Step](#PShellJob), [Command Prompt Job Step](#CmdExecJob)  
  
## <a name="before-you-begin"></a>开始之前  
 共有多种类型的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业步骤。 每种类型都与用来实现特定环境（如复制代理或命令提示环境）的子系统关联。 您可以对 Windows PowerShell 脚本进行编码，然后使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理将这些脚本包括在按计划时间运行或者为了响应 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件而运行的作业中。 可以使用命令提示作业步骤或 PowerShell 作业步骤运行 Windows PowerShell 脚本。  
  
1.  使用 PowerShell 作业步骤以便让 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理子系统运行 **模块的每个** 实用工具，该实用工具将启动 PowerShell 并导入 **模块的每个** 模块。  
  
2.  使用命令提示作业步骤以便运行 PowerShell.exe，并且指定导入 **sqlps** 模块的脚本。  
  
###  <a name="LimitationsRestrictions"></a> 限制和局限  
  
> [!CAUTION]  
>  运行 PowerShell 并且导入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sqlps **模块的每个** 代理作业步骤都将启动一个进程，该进程将占用大约 20 MB 的内存。 同时运行大量的 Windows PowerShell 作业步骤会对性能产生负面影响。  
  
##  <a name="PShellJob"></a> 创建 PowerShell 作业步骤  
 **创建 PowerShell 作业步骤**  
  
1.  展开“SQL Server 代理”，创建一个新作业或右键单击一个现有作业，再单击“属性”。 有关创建作业的详细信息，请参阅 [创建作业](http://msdn.microsoft.com/library/465fb7fc-7622-4252-a178-ea51691c935b)。  
  
2.  在 **“作业属性”** 对话框中，单击 **“步骤”** 页，再单击 **“新建”**。  
  
3.  在 **“新建作业步骤”** 对话框中，键入作业的 **“步骤名称”**。  
  
4.  在 **“类型”** 列表中单击 **PowerShell**。  
  
5.  在 **“运行身份”** 列表中，选择该作业将要使用的代理帐户和凭据。  
  
6.  在 **“命令”** 框中，输入将为该作业步骤执行的 PowerShell 脚本语法。 或者，单击 **“打开”** ，选择包含脚本语法的文件。  
  
7.  单击 **“高级”** 页设置以下作业步骤选项：当该作业步骤成功或失败时将执行的操作、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理应该尝试执行该作业步骤的次数以及重试的时间间隔。  
  
##  <a name="CmdExecJob"></a> 创建命令提示作业步骤  
 **创建 CmdExec 作业步骤**  
  
1.  展开“SQL Server 代理”，创建一个新作业或右键单击一个现有作业，再单击“属性”。 有关创建作业的详细信息，请参阅 [创建作业](http://msdn.microsoft.com/library/465fb7fc-7622-4252-a178-ea51691c935b)。  
  
2.  在 **“作业属性”** 对话框中，单击 **“步骤”** 页，再单击 **“新建”**。  
  
3.  在 **“新建作业步骤”** 对话框中，键入作业的 **“步骤名称”**。  
  
4.  在 **“类型”** 列表中，选择 **“操作系统(CmdExec)”**。  
  
5.  在 **“运行身份”** 列表中，选择具有作业将使用的凭据的代理帐户。 默认情况下，CmdExec 作业步骤在 SQL Server 代理服务帐户的上下文中运行。  
  
6.  在 **“成功命令的进程退出代码”** 框中，输入一个介于 0 到 999999 之间的值。  
  
7.  在 **“命令”** 框中，输入 powershell.exe 以及指定要运行的 PowerShell 脚本的参数。  
  
8.  单击 **“高级”** 页设置以下作业步骤选项，例如：当该作业步骤成功或失败时将执行的操作、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理应该尝试执行该作业步骤的次数，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理将作业步骤输出写入哪个文件。 只有 **sysadmin** 固定服务器角色的成员才可以将作业步骤输出写入到操作系统文件中。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
