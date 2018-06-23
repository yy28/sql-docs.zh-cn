---
title: 安装 SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 854c0b2f-02d2-46a4-a8cc-6b7a5d191cf8
caps.latest.revision: 6
author: mgblythe
ms.author: mblythe
manager: jhubbard
ms.openlocfilehash: 26ddefde6223effd90d2130c40c28011de411802
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123688"
---
# <a name="install-sql-server-powershell"></a>安装 SQL Server PowerShell
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果它检测到你选择的安装程序将停止[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]未安装功能，包括 PowerShell 组件，但 Windows PowerShell 2.0。 您必须通过使用 Windows Management Framework 安装 PowerShell，然后重新运行安装程序。  
  
## <a name="installing-includessnoversionincludesssnoversion-mdmd-powershell-support"></a>安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 支持  
 您通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序安装为 Windows PowerShell 提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持的软件。 当选择任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]功能需要 PowerShell 支持，安装程序将检查是否安装了 Windows PowerShell 2.0。 如果存在 PowerShell 2.0，则安装程序然后将安装下列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]PowerShell 组件：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 管理单元。这些管理单元是 dll 文件，可用来实现两种类型的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Windows PowerShell 支持：  
  
    -   一组 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cmdlet。 Cmdlet 是用来实现特定操作的命令。 例如， **Invoke-Sqlcmd** 可用于运行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或 XQuery 脚本，而这些脚本也可使用 **sqlcmd** 实用工具运行， **Invoke-PolicyEvaluation** 用于报告 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象是否符合基于策略的管理策略。  
  
    -   一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供程序。 通过该提供程序，可以使用类似于文件系统路径的路径，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象的层次结构中导航。 每个对象都与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理对象模型中的一个类关联。 您可以使用该类的方法和属性来针对对象执行工作。 例如，如果通过 cd 切换到路径中的某个数据库对象，则可以使用 Microsoft.SqlServer.Managment.SMO.Database 类的方法和属性来管理该数据库。  
  
-   **Sqlps**导入到 Windows PowerShell 2.0 会话中以便加载的模块[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]管理单元。  
  
-   不推荐使用**sqlps**实用程序，启动 Windows PowerShell 2.0 会话和导入**sqlps**模块。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 支持从对象资源管理器树启动 Windows PowerShell 会话。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理支持 Windows PowerShell 作业步骤。  
  
 如果 Windows PowerShell 2.0 未安装，或已被卸载，则必须安装它的说明[Windows Management Framework](http://go.microsoft.com/fwlink/?LinkId=186214)页。  
  
 安装程序完成后，则在卸载 Windows PowerShell [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows PowerShell 将不起作用的功能。 Windows PowerShell 可由 Windows 用户卸载，某些 Windows 操作系统升级可能会要求卸载 Windows PowerShell。 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 功能，您必须通过使用 Windows Management Framework 重新安装 PowerShell 2.0。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)  
  
  