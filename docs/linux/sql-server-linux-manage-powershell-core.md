---
title: 管理 Linux 上的 PowerShell Core 使用的 SQL Server
description: 本文提供了用于 Linux 上的 SQL Server 使用 PowerShell Core 的概述。
ms.date: 04/22/2019
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
author: SQLvariant
ms.author: aanelson
ms.reviewer: vanto
ms.openlocfilehash: d8d0675bbb7ebbedc9d1efec29fff8854670c10f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952539"
---
# <a name="manage-sql-server-on-linux-with-powershell-core"></a>管理 Linux 上的 PowerShell Core 使用的 SQL Server

本文介绍了[SQL Server PowerShell](../powershell/sql-server-powershell.md)并指导你完成几个有关如何使用 PowerShell Core （PS 核心） 使用的示例在 macOS 和 Linux 上。 PowerShell Core 目前一个开放源代码项目所在[GitHub](https://github.com/powershell/powershell)。

## <a name="cross-platform-editor-options"></a>跨平台编辑器选项

所有 PowerShell Core 下面的步骤将在正则终端中，或从 VS Code 或 Azure Data Studio 中的终端运行它们。  VS Code 和 Azure Data Studio 均可在 macOS 和 Linux 上。  Azure Data Studio 的详细信息，请参阅[本快速入门](https://docs.microsoft.com/sql/azure-data-studio/quickstart-sql-server)。  您可能还要考虑使用[PowerShell 扩展](https://docs.microsoft.com/sql/azure-data-studio/powershell-extension)它。

## <a name="installing-powershell-core"></a>安装 PowerShell Core

有关各种受支持的和试验性平台上安装 PowerShell Core 的详细信息，请参阅以下文章：

- [在 Windows 上安装 PowerShell Core](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-windows?view=powershell-6)
- [Linux 上安装 PowerShell Core](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6)
- [在 macOS 上安装 PowerShell Core](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6)
- [在 ARM 上安装 PowerShell Core](https://docs.microsoft.com/powershell/scripting/install/powershell-core-on-arm?view=powershell-6)

## <a name="install-the-sqlserver-module"></a>安装 SqlServer 模块

`SqlServer`模块中进行维护[PowerShell 库](https://www.powershellgallery.com/packages/SqlServer/)。 当使用 SQL Server 时，应始终使用 SqlServer PowerShell 模块的最新版本。

若要安装 SqlServer 模块，请打开 PowerShell Core 会话并运行以下代码：

```powerhsell
Install-Module -Name SqlServer
```

有关如何从 PowerShell 库安装 SqlServer 模块的详细信息，请参阅此[页](../powershell/download-sql-server-ps-module.md)。

## <a name="using-the-sqlserver-module"></a>使用 SqlServer 模块

让我们先启动 PowerShell Core。  如果你位于 macOS 或 Linux，打开*终端会话*上您的计算机，然后键入**pwsh**以启动新的 PowerShell Core 会话。  在 Windows 中，使用<kbd>赢取</kbd>+<kbd>R</kbd>，然后键入`pwsh`以启动新的 PowerShell Core 会话。

```
pwsh
```

SQL Server 提供了一个名为的 PowerShell 模块**SqlServer**。 可以使用**SqlServer**模块导入 PowerShell 环境或脚本的 SQL Server 组件 （SQL Server 提供程序和 cmdlet）。

复制并粘贴以下命令在 PowerShell 提示符下，若要导入**SqlServer**到当前 PowerShell 会话的模块：

```powershell
Import-Module SqlServer
```

若要验证的 PowerShell 提示符下键入以下命令**SqlServer**模块已正确导入：

```powershell
Get-Module -Name SqlServer
```

PowerShell 应显示类似于以下输出的信息：

```
ModuleType Version    Name          ExportedCommands
---------- -------    ----          ----------------
Script     21.1.18102 SqlServer     {Add-SqlAvailabilityDatabase, Add-SqlAvailabilityGroupList...
```

## <a name="connect-to-sql-server-and-get-server-information"></a>连接到 SQL Server 并获取服务器信息

以下步骤使用 PowerShell Core 来连接到 Linux 上的 SQL Server 实例，并显示几个服务器属性。

复制并粘贴以下命令在 PowerShell 提示符下。 运行这些命令时，PowerShell 将：
- 显示一个对话框，提示您输入的主机名或实例的 IP 地址
- 显示*PowerShell 凭据请求*对话框，提示你输入凭据。 可以使用你*SQL 用户名*并*SQL 密码*连接到 Linux 上的 SQL Server 实例
- 使用**Get SqlInstance** cmdlet 连接到**Server**并显示几个属性

（可选） 您只需替换`$serverInstance`变量与 IP 地址或主机名的 SQL Server 实例。

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Connect to the Server and return a few properties
Get-SqlInstance -ServerInstance $serverInstance -Credential $credential
# done
```

PowerShell 应显示类似于以下输出的信息：

```
Instance Name                   Version    ProductLevel UpdateLevel  HostPlatform HostDistribution
-------------                   -------    ------------ -----------  ------------ ----------------
your_server_instance            14.0.3048  RTM          CU13         Linux        Ubuntu
```

> [!NOTE]
> 如果没有显示这些值的内容，与目标 SQL Server 实例的连接可能已失败。 请确保可以使用相同的连接信息从 SQL Server Management Studio 进行连接。 然后查看[连接故障排除建议](sql-server-linux-troubleshooting-guide.md#connection)。

## <a name="using-the-sql-server-powershell-provider"></a>使用 SQL Server PowerShell 提供程序

用于连接到 SQL Server 实例的另一个选项是使用[SQL Server PowerShell 提供程序](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider)。  使用提供程序，可导航像您已在对象资源管理器，但命令行在树结构中导航到类似的 SQL Server 实例。  默认情况下此提供程序显示为名为 PSDrive`SQLSERVER:\`可以用于连接和导航您的域帐户有权的 SQL Server 实例。  请参阅[配置步骤](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-auth-overview#configuration-steps)有关如何安装 Linux 上的 SQL Server 的 Active Directory 身份验证的信息。

此外可以使用 SQL Server PowerShell 提供程序使用 SQL 身份验证。 若要执行此操作，请使用`New-PSDrive`cmdlet 来创建新的 PSDrive，提供用于连接的正确凭据。

在此示例中，您将看到如何创建新的 PSDrive 使用 SQL 身份验证的示例。

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.

New-PSDrive -Name SQLonDocker -PSProvider SqlServer -Root 'SQLSERVER:\SQL\localhost,10002\Default\' -Credential $credential
```

你可以确认运行时创建的驱动器`Get-PSDrive`cmdlet。

```powershell
Get-PSDrive
```

创建新的 PSDrive 之后, 可以开始导航它。

```powershell
dir SQLonDocker:\Databases
```

下面是输出可能如下所示。  您可能注意到此输出结果类似于 SSMS 将显示在数据库节点。  它将显示用户数据库，但不是系统数据库。

```powershell
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2016   Normal      209.63 MB    1.31 MB Simple       130 sa
AdventureWorksDW2012 Normal      167.00 MB   32.47 MB Simple       110 sa
AdventureWorksDW2014 Normal      188.00 MB   78.10 MB Simple       120 sa
AdventureWorksDW2016 Normal      172.00 MB   74.76 MB Simple       130 sa
AdventureWorksDW2017 Normal      208.00 MB   40.57 MB Simple       140 sa
```

如果你需要查看您的实例上的所有数据库，一种方法是使用`Get-SqlDatabase`cmdlet。

## <a name="get-databases"></a>获取数据库

若要了解重要的 cmdlet 是`Get-SqlDatabase`。  对于涉及到一个数据库或在数据库中，对象的许多操作`Get-SqlDatabase`，可以使用 cmdlet。  如果您提供两个值`-ServerInstance`和`-Database`将检索参数，仅该一个数据库对象。  但是，如果仅指定`-ServerInstance`参数，将返回该实例上的所有数据库的完整列表。

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.

# Connect to the Instance and retrieve all databases
Get-SqlDatabase -ServerInstance ServerB -Credential $credential
```

下面是通过上述 Get-sqldatabase 命令可能返回的内容的一个示例：

```powershell
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2016   Normal      209.63 MB    1.31 MB Simple       130 sa
AdventureWorksDW2012 Normal      167.00 MB   32.47 MB Simple       110 sa
AdventureWorksDW2014 Normal      188.00 MB   78.10 MB Simple       120 sa
AdventureWorksDW2016 Normal      172.00 MB   74.88 MB Simple       130 sa
AdventureWorksDW2017 Normal      208.00 MB   40.63 MB Simple       140 sa
master               Normal        6.00 MB  600.00 KB Simple       140 sa
model                Normal       16.00 MB    5.70 MB Full         140 sa
msdb                 Normal       15.50 MB    1.14 MB Simple       140 sa
tempdb               Normal       16.00 MB    5.49 MB Simple       140 sa

```

## <a name="examine-sql-server-error-logs"></a>检查 SQL Server 错误日志

以下步骤使用 PowerShell Core 来检查连接 Linux 上的 SQL Server 实例的日志的错误。

复制并粘贴以下命令在 PowerShell 提示符下。 它们可能会运行几分钟。 这些命令执行以下步骤：
- 显示一个对话框，提示您输入的主机名或实例的 IP 地址
- 显示*PowerShell 凭据请求*对话框，提示您输入的凭据。 可以使用你*SQL 用户名*并*SQL 密码*连接到 Linux 上的 SQL Server 实例
- 使用**Get-sqlerrorlog** cmdlet 来连接到 Linux 上的 SQL Server 实例并检索错误日志以来**昨天**

（可选） 可以替换`$serverInstance`变量与 IP 地址或主机名的 SQL Server 实例。

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday
# done
```

## <a name="explore-cmdlets-currently-available-in-ps-core"></a>探索 PS Core 中当前可用的 cmdlet
SqlServer 模块当前有 106 cmdlet 可在 Windows PowerShell，而仅 59 的 106 PSCore 中提供了。 下面包含了当前可用的 59 cmdlet 的完整列表。  SqlServer 模块中的所有 cmdlet 的详细文档，请参阅 SqlServer [cmdlet 参考](https://docs.microsoft.com/powershell/module/sqlserver/)。

以下命令将显示您的所有可用 cmdlet 上使用的 PowerShell 的版本。

```powershell
Get-Command -Module SqlServer -CommandType Cmdlet |
SORT -Property Noun |
SELECT Name
```

- ConvertFrom-EncodedSqlName
- ConvertTo-EncodedSqlName
- Get-SqlAgent
- Get-SqlAgentJob
- Get-SqlAgentJobHistory
- Get-SqlAgentJobSchedule
- Get-SqlAgentJobStep
- Get-SqlAgentSchedule
- Remove-SqlAvailabilityDatabase
- Resume-SqlAvailabilityDatabase
- Add-SqlAvailabilityDatabase
- Suspend-SqlAvailabilityDatabase
- New-SqlAvailabilityGroup
- Set-SqlAvailabilityGroup
- Remove-SqlAvailabilityGroup
- Switch-SqlAvailabilityGroup
- Join-SqlAvailabilityGroup
- Revoke-SqlAvailabilityGroupCreateAnyDatabase
- Grant-SqlAvailabilityGroupCreateAnyDatabase
- New-SqlAvailabilityGroupListener
- Set-SqlAvailabilityGroupListener
- Add-SqlAvailabilityGroupListenerStaticIp
- Set-SqlAvailabilityReplica
- Remove-SqlAvailabilityReplica
- New-SqlAvailabilityReplica
- Set-SqlAvailabilityReplicaRoleToSecondary
- New-SqlBackupEncryptionOption
- Get-SqlBackupHistory
- Invoke-Sqlcmd
- New-SqlCngColumnMasterKeySettings
- Remove-SqlColumnEncryptionKey
- Get-SqlColumnEncryptionKey
- Remove-SqlColumnEncryptionKeyValue
- Add-SqlColumnEncryptionKeyValue
- Get-SqlColumnMasterKey
- Remove-SqlColumnMasterKey
- New-SqlColumnMasterKey
- Get-SqlCredential
- Set-SqlCredential
- New-SqlCredential
- Remove-SqlCredential
- New-SqlCspColumnMasterKeySettings
- Get-SqlDatabase
- Restore-SqlDatabase
- Backup-SqlDatabase
- Set-SqlErrorLog
- Get-SqlErrorLog
- New-SqlHADREndpoint
- Set-SqlHADREndpoint
- Get-SqlInstance
- Add-SqlLogin
- Remove-SqlLogin
- Get-SqlLogin
- Set-SqlSmartAdmin
- Get-SqlSmartAdmin
- Read-SqlTableData
- Write-SqlTableData
- Read-SqlViewData
- Convert-UrnToPath

## <a name="see-also"></a>请参阅
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
