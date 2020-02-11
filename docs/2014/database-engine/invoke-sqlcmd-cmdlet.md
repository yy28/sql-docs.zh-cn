---
title: Invoke-Sqlcmd cmdlet | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- PowerShell [SQL Server], Invoke-Sqlcmd
- Cmdlets [SQL Server], Invoke-Sqlcmd
- Invoke-Sqlcmd cmdlet
- sqlcmd utility, PowerShell
ms.assetid: 0c74d21b-84a5-4fa4-be51-90f0f7230044
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: beee2fa576387eadb75ee5ab1bfefcb66453acc0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "76928025"
---
# <a name="invoke-sqlcmd-cmdlet"></a>Invoke-Sqlcmd cmdlet
  **Invoke-Sqlcmd**是一个[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cmdlet，它运行的脚本包含来自各种语言（[!INCLUDE[tsql](../includes/tsql-md.md)]和 XQuery）和**Sqlcmd**实用工具所支持的命令的语句。  
  
## <a name="using-invoke-sqlcmd"></a>使用 Invoke-Sqlcmd  
 
  **Invoke-Sqlcmd** cmdlet 可使你在 Windows PowerShell 环境中运行 **sqlcmd** 。 用 **sqlcmd** 执行的大部分操作也可以通过使用 **Invoke-sqlcmd**来完成。  
  
 下面的示例说明如何通过调用 Invoke-Sqlcmd 来执行简单查询，这与指定带有 **-Q** 和 **-S** 选项的 **sqlcmd** 相似：  
  
```powershell
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance"  
```  
  
 下面的示例说明如何调用 **Invoke-Sqlcmd**、指定输入文件并将输出发送到一个文件中，这与指定带有 **-i** 和 **-o** 选项的 **sqlcmd** 相似：  
  
```powershell
Invoke-Sqlcmd -InputFile "C:\MyFolder\TestSQLCmd.sql" | Out-File -FilePath "C:\MyFolder\TestSQLCmd.rpt"  
```  
  
 下面的示例说明如何使用 Windows PowerShell 数组来将多个 **sqlcmd** 脚本变量传递到 **Invoke-Sqlcmd**。 用于标识 SELECT 语句中 **sqlcmd** 脚本变量的“$”字符已经通过使用 PowerShell 反引号“`”转义符进行转义：  
  
```powershell
$MyArray = "MyVar1 = 'String1'", "MyVar2 = 'String2'"  
Invoke-Sqlcmd -Query "SELECT `$(MyVar1) AS Var1, `$(MyVar2) AS Var2;" -Variable $MyArray  
```  
  
 下面的示例说明如何使用 Windows PowerShell 的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供程序导航到 [!INCLUDE[ssDE](../includes/ssde-md.md)]实例，然后使用 Windows PowerShell **Get-Item** cmdlet 检索该实例的 SMO Server 对象并将它传递到 **Invoke-Sqlcmd**：  
  
```powershell
Set-Location SQLSERVER:\SQL\MyComputer\MyInstance  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance (Get-Item .)  
```  
  
 -Query 参数是位置参数，不需要命名。 如果传递到 **Invoke-Sqlcmd**的第一个字符串没有命名，则将其视为 -Query 参数处理。  
  
```powershell
Invoke-Sqlcmd "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance"  
```  
  
## <a name="path-context-in-invoke-sqlcmd"></a>Invoke-Sqlcmd 中的路径上下文  
 如果没有使用 -Database 参数，则 Invoke-Sqlcmd 的数据库上下文由调用 cmdlet 时的活动路径设置。  
  
|路径|数据库上下文|  
|----------|----------------------|  
|从 SQLSERVER 以外的驱动器开始：|本地计算机上默认实例中登录 ID 的默认数据库。|  
|SQLSERVER:\SQL|本地计算机上默认实例中登录 ID 的默认数据库。|  
|SQLSERVER:\SQL\ComputerName|指定计算机上默认实例中登录 ID 的默认数据库。|  
|SQLSERVER:\SQL\ComputerName\InstanceName|指定计算机上指定实例中登录 ID 的默认数据库。|  
|SQLSERVER:\SQL\ComputerName\InstanceName\Databases|指定计算机上指定实例中登录 ID 的默认数据库。|  
|SQLSERVER:\SQL\ComputerName\InstanceName\Databases\DatabaseName|指定计算机上指定实例中的指定数据库。 这也适用于较长的路径，例如指定数据库中的表和列节点的路径。|  
  
 例如，假定在本地计算机的默认实例中，您的 Windows 帐户的默认数据库是 master。 那么，以下命令将返回 master：  
  
```powershell
Set-Location SQLSERVER:\SQL  
Invoke-Sqlcmd "SELECT DB_NAME() AS DatabaseName;"  
```  
  
 以下命令将返回 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]：  
  
```powershell
Set-Location SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012\Tables\Person.Person  
Invoke-Sqlcmd "SELECT DB_NAME() AS DatabaseName;"  
```  
  
 当 Invoke-Sqlcmd 使用路径数据库上下文时，它会提供一条警告。 可以使用 -SuppressProviderContextWarning 参数来关闭该警告消息。 可以使用 -IgnoreProviderContext 参数来通知 Invoke-Sqlcmd 始终使用登录帐户的默认数据库。  
  
## <a name="comparing-invoke-sqlcmd-and-the-sqlcmd-utility"></a>Invoke-Sqlcmd 和 sqlcmd 实用工具的比较  
 **Invoke-Sqlcmd**可用于运行多个可以使用**Sqlcmd**实用程序运行的脚本。 但是，用来运行 **Invoke-Sqlcmd** 的 Windows PowerShell 环境不同于用来运行 **sqlcmd** 的命令提示环境。 为了使 **Invoke-Sqlcmd** 在 Windows PowerShell 环境中有效，已对其行为进行了修改。  
  
 并非所有的 **sqlcmd** 命令都已在 **Invoke-Sqlcmd**中实现。 未实现的命令包括：**:!!**、**:connect**、**:error****:out**、**:ed**、**:list**、**:listvar**、**:reset**、**:perftrace** 和 **:serverlist**。  
  
 **Invoke-sqlcmd**不会初始化**Sqlcmd**环境或脚本变量，如 SQLCMDDBNAME 或 SQLCMDWORKSTATION。  
  
 **调用-Sqlcmd**不显示消息（如 PRINT 语句的输出），除非指定 Windows PowerShell **-Verbose**通用参数。 例如：  
  
```powershell
Invoke-Sqlcmd -Query "PRINT N'abc';" -Verbose  
```  
  
 并非所有的 **sqlcmd** 参数都需要在 PowerShell 环境中使用。 例如，Windows PowerShell 设置所有 cmdlet 输出的格式，因此，指定格式选项的 **sqlcmd** 参数将不能在 **Invoke-Sqlcmd**中实现。 下表显示了**Invoke-Sqlcmd**参数和**Sqlcmd**选项之间的关系：  
  
|说明|sqlcmd 选项|Invoke-Sqlcmd 参数|  
|-----------------|-------------------|------------------------------|  
|服务器名称和实例名称|-S|-ServerInstance|  
|要使用的初始数据库|-d|-Database|  
|运行指定的查询并退出|-S|-Query|  
|
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证登录 ID|-U|-Username|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]身份验证密码。|-P|-Password|  
|变量定义|-v|-Variable|  
|查询超时间隔|-t|-QueryTimeout|  
|在遇到错误时停止运行|-b|-AbortOnError|  
|专用管理员连接|-A|-DedicatedAdministratorConnection|  
|禁用交互式命令、启动脚本和环境变量|-x|-DisableCommands|  
|禁用变量替换|-x|-DisableVariables|  
|要报告的最小严重级别|-v|-SeverityLevel|  
|要报告的最小错误级别|-M|-ErrorLevel|  
|登录超时间隔|-l|-ConnectionTimeout|  
|主机名|-h|-HostName|  
|更改密码并退出|-Z|-NewPassword|  
|包含查询的输入文件|-i|-InputFile|  
|字符输出的最大长度|-w|-MaxCharLength|  
|二进制输出的最大长度|-w|-MaxBinaryLength|  
|使用 SSL 加密机制进行连接|无参数|-EncryptConnection|  
|显示错误|无参数|-OutputSqlErrors|  
|将消息输出到 stderr|-r|无参数|  
|使用客户端的区域设置|-R|无参数|  
|运行指定的查询并保持运行状态|-q|无参数|  
|要用于输出数据的代码页|-f|无参数|  
|更改密码并保持运行状态|-Z|无参数|  
|数据包大小|-a|无参数|  
|列分隔符|-s|无参数|  
|控制输出标头|-h|无参数|  
|指定控制字符|-k|无参数|  
|长度固定的显示宽度|-y|无参数|  
|长度可变的显示宽度|-y|无参数|  
|回显输入|-E|无参数|  
|允许使用带引号的标识符|-I|无参数|  
|删除尾随空格|-W|无参数|  
|列出实例|-l|无参数|  
|将输出格式化为 Unicode|-u|无参数|  
|打印统计信息|-p|无参数|  
|结束命令|-c|无参数|  
|使用 Windows 身份验证进行连接|-e|无参数|  
  
## <a name="see-also"></a>另请参阅  
 [使用数据库引擎 cmdlet](../../2014/database-engine/use-the-database-engine-cmdlets.md)   
 [sqlcmd 实用工具](../tools/sqlcmd-utility.md)   
 [使用 sqlcmd 实用工具](../relational-databases/scripting/sqlcmd-use-the-utility.md)  
