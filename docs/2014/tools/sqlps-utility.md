---
title: sqlps 实用工具 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- sqlps utility
- PowerShell [SQL Server], sqlps utility
ms.assetid: 4b2515a6-12c3-44fb-b263-1c567681cd2b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b25921a7b48ecd818527dd95ebc2d8714cb6871d
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59241507"
---
# <a name="sqlps-utility"></a>sqlps 实用工具
  `sqlps` 实用工具会启动一个 Windows PowerShell 2.0 会话，并加载和注册 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 提供程序和 cmdlet。 您可以输入 PowerShell 命令或脚本，它们使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 组件来处理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的实例及其对象。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)]请改用 `sqlps` PowerShell 模块。 有关详细信息`sqlps`模块，请参阅[导入 SQLPS 模块](../database-engine/import-the-sqlps-module.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
      sqlps   
[ [ [ -NoLogo ][ -NoExit ][ -NoProfile ]  
    [ -OutPutFormat { Text | XML } ] [ -InPutFormat { Text | XML } ]  
  ]  
  [ -Command { -  
             | script_block [ -argsargument_array ]  
             | string [ command_parameters ]  
             }  
  ]  
]  
[ -? | -Help ]  
```  
  
## <a name="arguments"></a>参数  
 **-NoLogo**  
 指定 `sqlps` 实用工具在启动时隐藏版权标志。  
  
 **-NoExit**  
 指定 `sqlps` 实用工具在完成启动命令后仍继续运行。  
  
 **-NoProfile**  
 指定 `sqlps` 实用工具不加载用户配置文件。 用户配置文件记录 PowerShell 会话期间常用的别名、函数和变量。  
  
 **-OutPutFormat** { **Text** | **XML** }  
 指定的`sqlps`实用工具的输出格式化为文本字符串 (**文本**) 或序列化的 CLIXML 格式 (**XML**)。  
  
 **-InPutFormat** { **Text** | **XML** }  
 指定的输入`sqlps`实用程序文本字符串格式 (**文本**) 或序列化的 CLIXML 格式 (**XML**)。  
  
 **-Command**  
 指定要使 `sqlps` 实用工具运行的命令。 `sqlps`实用工具运行命令，然后退出，除非 **-NoExit**还指定了。 请不要在 **-Command**后指定任何其他开关，如果指定，它们将被读作命令参数。  
  
 **-**  
 **-Command-** 指定`sqlps`实用工具从标准输入读取输入。  
  
 *script_block* [ **-args**_argument_array_ ]  
 指定要运行的 PowerShell 命令块，块必须用大括号 {} 括起来。 *Script_block*仅当指定`sqlps`实用程序称为眖**PowerShell**或另一个`sqlps`实用工具会话。 *Argument_array* 是 PowerShell 变量的数组，包含 *script_block*中 PowerShell 命令的参数。  
  
 *字符串* [ *command_parameters* ]  
 指定包含要运行的 PowerShell 命令的字符串。 使用格式 **"& {*`command`*}"**。 引号指示一个字符串，并调用运算符 (&) 的原因`sqlps`实用工具来运行该命令。  
  
 [ **-?** | **-Help** ]  
 显示 `sqlps` 实用工具选项的语法摘要。  
  
## <a name="remarks"></a>备注  
 `sqlps`实用工具启动 PowerShell 环境 (PowerShell.exe) 并加载[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]PowerShell 模块。 该模块，也称为`sqlps`，然后加载并注册以下[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]PowerShell 管理单元：  
  
-   Microsoft.SqlServer.Management.PSProvider.dll  
  
     实现 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 提供程序和关联的 cmdlets，如 **Encode-SqlName** 和 **Decode-SqlName**。  
  
-   Microsoft.SqlServer.Management.PSSnapin.dll  
  
     实现 **Invoke-Sqlcmd** 和 **Invoke-PolicyEvaluation** cmdlets。  
  
 可以使用 `sqlps` 实用工具执行下列操作：  
  
-   以交互方式运行 PowerShell 命令。  
  
-   运行 PowerShell 脚本文件。  
  
-   运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cmdlet。  
  
-   使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供程序路径可以浏览 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 对象的层次结构。  
  
 默认情况下`sqlps`实用工具在运行脚本的执行策略设置为**Restricted**。 这样可以防止运行任何 PowerShell 脚本。 可以使用 **Set-ExecutionPolicy** cmdlet 来启用运行签名的脚本或任意脚本。 请仅运行来自受信任源的脚本，并通过使用适当的 NTFS 权限来保证所有输入和输出文件的安全。 有关启用 PowerShell 脚本的详细信息，请参阅 [Running Windows PowerShell Scripts](https://www.tech-recipes.com/rx/2513/powershell_enable_script_support/)（运行 Windows PowerShell 脚本）。  
  
 在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 和 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 中，此 `sqlps` 实用工具版本已作为 Windows PowerShell 1.0 微型 shell 实现。 微型外壳程序具有某些限制，例如不允许用户加载不是由微型外壳程序所加载的管理单元。 这些限制并不适用于 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 版本及更高的版本的实用工具，这些版本已更改为使用 `sqlps` 模块。  
  
## <a name="examples"></a>示例  
 **A.以默认的交互模式运行 sqlps 实用工具，不显示版权标志**  
  
```  
sqlps -NoLogo  
```  
  
 **B.从命令提示符下运行 SQL Server PowerShell 脚本**  
  
```  
sqlps -Command "&{.\MyFolder.MyScript.ps1}"  
```  
  
 **C.从命令提示符下运行 SQL Server PowerShell 脚本，并在脚本完成后继续运行**  
  
```  
sqlps -NoExit -Command "&{.\MyFolder.MyScript.ps1}"  
```  
  
## <a name="see-also"></a>请参阅  
 [启用或禁用服务器网络协议](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)  
  
  
