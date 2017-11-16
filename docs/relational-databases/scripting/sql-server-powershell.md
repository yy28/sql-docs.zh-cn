---
title: SQL Server PowerShell | Microsoft Docs
ms.custom: 
ms.date: 08/04/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 2007b572b659f5fe9371618b667bb27a43bc70c8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-powershell"></a>SQL Server PowerShell
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支持 Windows PowerShell，Windows PowerShell 是一个功能强大的脚本 shell，管理员和开发人员可以通过它自动执行服务器管理和应用程序部署。 与 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本相比，Windows PowerShell 语言能够支持更复杂的逻辑，这使得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员能够生成强大的管理脚本。 Windows PowerShell 脚本还可用来管理其他 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 服务器产品， 这为管理员提供一个跨服务器的公用脚本语言。  
  
## <a name="sql-server-powershell-components"></a>SQL Server PowerShell 组件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了一个名为 **sqlps** 的 Windows PowerShell 模块，用于将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件导入 Windows PowerShell 环境或脚本中。 **sqlps** 模块加载两个可用来实现以下内容的 Windows PowerShell 管理单元：  
  
-   一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供程序（允许使用类似于文件系统路径的简单导航机制）。 您可以生成类似于文件系统路径的路径，在该路径中，驱动器与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理对象模型关联，节点基于对象模型类。 然后，你可以使用熟悉的命令（如 **cd** 和 **dir** ），按照在命令提示符窗口中导航文件夹的类似方式导航路径。 可以使用其他命令（如 **ren** 或 **del**）对路径中的节点执行操作。  
  
-   一组 cmdlet（它们在 Windows PowerShell 脚本中用于指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 操作）。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cmdlet 支持各种操作，如运行包含 **或 XQuery 语句的** sqlcmd [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本。  
  
 若要了解有关 Windows PowerShell 的信息，请参阅 [Windows PowerShell 入门](https://msdn.microsoft.com/powershell/scripting/getting-started/getting-started-with-windows-powershell)。  
  
## <a name="sql-server-versions"></a>SQL Server 版本  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] PowerShell 组件可用于管理 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 或更高版本的实例。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 的实例必须运行 SP2 或更高版本。 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 的实例必须运行 SP4 或更高版本。 将 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] PowerShell 组件与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的早期版本一起使用时，这些组件的功能将限制为在那些版本中提供的功能。  
     
## <a name="sql-server-powershell-tasks"></a>SQL Server PowerShell 任务  
  
|任务说明|主题|  
|----------------------|-----------| 
|安装 Microsoft® Windows PowerShell Extensions for Microsoft [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  安装 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，将默认安装 PowerShell 模块。  可以通过从 Microsoft® SQL Server® 2016 功能包中安装以下组件来手动安装 PowerShell Extensions for SQL Server 2016：<br/>     Microsoft® System CLR Types for Microsoft SQL Server® 2016 (SQLSysClrTypes.msi)<br/>Microsoft® SQL Server® 2016 共享管理对象 (SharedManagementObjects.msi)<br/> Microsoft® Windows PowerShell Extensions for Microsoft SQL Server® 2016 (PowerShellTools.msi)|[Microsoft® SQL Server® 2016 功能包](https://www.microsoft.com/en-us/download/details.aspx?id=52676)。   | 
|介绍用于运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 组件、打开 PowerShell 会话和加载 **sqlps** 模块的首选机制。 **sqlps** 模块在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 提供程序和 cmdlet 以及该提供程序和 cmdlet 使用的 SQL Server 管理对象 (SMO) 程序集中加载。|[导入 SQLPS 模块](../../relational-databases/scripting/import-the-sqlps-module.md)|  
|介绍如何仅加载 SMO 程序集而不加载提供程序或 cmdlet。|[在 Windows PowerShell 中加载 SMO 程序集](../../relational-databases/scripting/load-the-smo-assemblies-in-windows-powershell.md)|  
|介绍如何通过右键单击“对象资源管理器”中的节点来运行 Windows PowerShell 会话。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 启动 Windows PowerShell 会话，加载 **sqlps** 模块，并将 SQL Server 提供程序路径设置为选定的对象。|[从 SQL Server Management Studio 中运行 Windows PowerShell](../../relational-databases/scripting/run-windows-powershell-from-sql-server-management-studio.md)|  
|介绍如何创建运行 Windows PowerShell 脚本的 SQL Server 代理作业步骤。 然后，可以将作业安排在特定时间或响应事件时运行。|[在 SQL Server 代理中运行 Windows PowerShell 步骤](../../relational-databases/scripting/run-windows-powershell-steps-in-sql-server-agent.md)|  
|介绍如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供程序浏览 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象的层次结构。|[SQL Server PowerShell 提供程序](../../relational-databases/scripting/sql-server-powershell-provider.md)|  
|介绍如何使用指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 操作（如运行 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 脚本）的 [!INCLUDE[tsql](../../includes/tsql-md.md)] cmdlet。|[使用数据库引擎 cmdlet](../../relational-databases/scripting/use-the-database-engine-cmdlets.md)|  
|介绍如何指定包含 Windows PowerShell 不支持的字符的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分隔标识符。|[PowerShell 中的 SQL Server 标识符](../../relational-databases/scripting/sql-server-identifiers-in-powershell.md)|  
|介绍如何建立 SQL Server 身份验证连接。 默认情况下，SQL Server PowerShell 组件使用 Windows 身份验证连接，该连接使用运行 Windows PowerShell 的进程的 Windows 凭据。|[在数据库引擎 PowerShell 中管理身份验证](../../relational-databases/scripting/manage-authentication-in-database-engine-powershell.md)|  
|介绍如何使用由 SQL Server PowerShell 提供程序实现的变量来控制使用 Windows PowerShell Tab 填写功能时列出的对象数。 当处理包含大量对象的数据库时，这一点特别有用。|[管理 Tab 自动补全 (SQL Server PowerShell)](../../relational-databases/scripting/manage-tab-completion-sql-server-powershell.md)|  
|介绍如何使用 Get-Help 以获取有关 Windows PowerShell 环境中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件的信息。|[获取 SQL Server PowerShell 帮助](../../relational-databases/scripting/get-help-sql-server-powershell.md)|  
  
  
