---
title: SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 08/04/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: scripting
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9eeb40333c719288af19655b61fdebeb88faa370
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
---
# <a name="sql-server-powershell"></a>SQL Server PowerShell
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

**[安装 SQL Server PowerShell](download-sql-server-ps-module.md)**

> [!NOTE]
> SQL Server PowerShell 模块有两种；SqlServer 和 SQLPS。 虽然 SQL Server 安装附带了 SQLPS 模块（用于向后兼容），但该模块不再更新。 最新的 PowerShell 模块是 SqlServer 模块。 SqlServer 模块不仅包含 SQLPS 更新版本的 cmdlet，并且还包含新的 cmdlet 以支持最新的 SQL 功能。  
> 虽然 SQL Server Management Studio (SSMS) 随附了以前版本的 SqlServer 模块，但仅限 16.x 版本的 SSMS。 要在 SSMS 17.0 和更高版本中使用 PowerShell，则必须从 PowerShell 库安装 SqlServer 模块。
> 要安装 SqlServer 模块，请参阅[安装 SQL Server PowerShell](download-sql-server-ps-module.md)。

**为什么模块从 SQLPS 更改为 SqlServer？**

要发送 SQL PowerShell 更新，必须更改 SQL PowerShell 模块的标识和名为 SQLPS.exe 的包装器。 由于此更改，现存在两种 SQL PowerShell 模块：SqlServer 模块和 SQLPS 模块。  

**若导入 SQLPS 模块，请更新 PowerShell 脚本。**

如果具有任何运行 `Import-Module -Name SQLPS` 的 PowerShell 脚本，并希望利用新的提供程序功能和新的 cmdlet，则必须将它们更改为 `Import-Module -Name SqlServer`。 新模块会安装到 `%ProgramFiles%\WindowsPowerShell\Modules\SqlServer` 文件夹。 因此，不需要更新 $env:PSModulePath 变量。 如果脚本使用名为 SqlServer 的第三方或社区版本模块，请使用 Prefix 参数以避免名称冲突。 SQL Server 代理使用的模块不做任何更改。 

  
## <a name="sql-server-powershell-components"></a>SQL Server PowerShell 组件  
SqlServer 模块加载两个 Windows PowerShell 管理单元：  
  
-   一个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供程序（允许使用类似于文件系统路径的简单导航机制）。 您可以生成类似于文件系统路径的路径，在该路径中，驱动器与 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理对象模型关联，节点基于对象模型类。 然后，你可以使用熟悉的命令（如 **cd** 和 **dir** ），按照在命令提示符窗口中导航文件夹的类似方式导航路径。 可以使用其他命令（如 **ren** 或 **del**）对路径中的节点执行操作。  
  
-   一组 cmdlet，它支持运行包含 [!INCLUDE[tsql](../includes/tsql-md.md)] 或 XQuery 语句的 sqlcmd 脚本等操作。  
  
  
## <a name="sql-server-versions"></a>SQL Server 版本  
SQL PowerShell cmdlet 可用于管理 Azure SQL 数据库、Azure SQL 数据仓库和所有[支持的 SQL Server 产品](https://support.microsoft.com/lifecycle/search/1044)的实例。  


## <a name="sql-server-identifiers-that-contain-characters-not-supported-in-powershell-paths"></a>包含 PowerShell 路径中不支持的字符的 SQL Server 标识符  
 
**Encode-Sqlname** 和 **Decode-Sqlname** cmdlet 帮助你指定包含 PowerShell 路径中不支持的字符的 SQL Server 标识符。 有关详细信息，请参阅 [SQL Server Identifiers in PowerShell](sql-server-identifiers-in-powershell.md)。  
  
使用 **Convert-UrnToPath** cmdlet 将 [!INCLUDE[ssDE](../includes/ssde-md.md)] 对象的统一资源名称转换为 SQL Server PowerShell 提供程序的路径。 有关详细信息，请参阅 [Convert URNs to SQL Server Provider Paths](https://docs.microsoft.com/powershell/module/sqlserver/Convert-UrnToPath)。  
  
## <a name="query-expressions-and-unique-resource-names"></a>查询表达式和唯一资源名称  

查询表达式是使用与 XPath 类似的语法指定一组条件的字符串，用于枚举对象模型层次结构中的一个或多个对象。 唯一资源名称 (URN) 是一种特定类型的查询表达式字符串，用于唯一标识单个对象。 有关详细信息，请参阅 [Query Expressions and Uniform Resource Names](query-expressions-and-uniform-resource-names.md)。       


## <a name="cmdlet-reference"></a>Cmdlet 引用
* [SqlServer cmdlet](https://docs.microsoft.com/powershell/module/sqlserver)
* [SQLPS cmdlet](https://docs.microsoft.com/powershell/module/sqlps)
