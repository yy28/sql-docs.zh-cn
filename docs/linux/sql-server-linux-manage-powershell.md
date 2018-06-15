---
title: 管理使用 PowerShell 的 Linux 上的 SQL Server |Microsoft 文档
description: 本文概述了在 Linux 上使用 SQL Server 的 Windows 上使用 PowerShell。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: a3492ce1-5d55-4505-983c-d6da8d1a94ad
ms.openlocfilehash: 54892a66cea7643d708bcd7ba5cf1b6b07d4523f
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
ms.locfileid: "34323668"
---
# <a name="use-powershell-on-windows-to-manage-sql-server-on-linux"></a>使用 Windows 上的 PowerShell 管理 Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍[SQL Server PowerShell](https://msdn.microsoft.com/en-us/library/mt740629.aspx)并指导您完成几个示例如何将它用于在 Linux 上的 SQL Server 2017。 Windows 上目前支持适用于 SQL Server 的 PowerShell，因此当 Windows 计算机连接到 Linux 上的远程 SQL Server 实例时，可以使用 PowerShell。

## <a name="install-the-newest-version-of-sql-powershell-on-windows"></a>在 Windows 上安装最新版本的 SQL PowerShell

[SQL PowerShell](https://msdn.microsoft.com/en-us/library/mt740629.aspx)在 Windows 上是附带[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)。 使用 SQL Server 时，应始终使用最新版本的 SSMS 和 SQL PowerShell。 最新版本的 SSMS 不断更新和优化并且当前适用于 SQL Server 2017 on Linux。 若要下载并安装最新版本，请参阅[下载 SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。 为保持使用最新版本，有可供下载的新版本时，最新版本的 SSMS 会发出提示。

## <a name="before-you-begin"></a>開始之前

读取[已知问题](sql-server-linux-release-notes.md)在 Linux 上的 SQL server 自 2017 年。

## <a name="launch-powershell-and-import-the-sqlserver-module"></a>启动 PowerShell 并导入*sqlserver*模块

首先在 Windows 上启动 PowerShell。 打开*命令提示符*上你的 Windows 计算机和类型**PowerShell**以启动新的 Windows PowerShell 会话。

```
PowerShell
```

SQL Server 提供了一个名为的 Windows PowerShell 模块**SqlServer** ，你可以使用导入 SQL Server 组件 （SQL Server 提供程序和 cmdlet） 到 PowerShell 环境或脚本。

复制并粘贴以下命令在 PowerShell 提示符下，若要导入**SqlServer**到当前 PowerShell 会话的模块：

```powershell
Import-Module SqlServer
```

若要验证的 PowerShell 提示符下键入以下命令**SqlServer**模块已正确导入：

```powershell
Get-Module -Name SqlServer
```

PowerShell 应显示类似于下面的输出的信息：

```
ModuleType Version    Name          ExportedCommands
---------- -------    ----          ----------------
Script     0.0        SqlServer
Manifest   20.0       SqlServer     {Add-SqlAvailabilityDatabase, Add-SqlAvailabilityGroupList...
```

## <a name="connect-to-sql-server-and-get-server-information"></a>连接到 SQL Server 并获取服务器信息

使用 Windows 上的 PowerShell 连接到 Linux 上的 SQL Server 2017 实例，并显示几个服务器属性。

复制并粘贴以下命令在 PowerShell 提示符。 运行这些命令时，PowerShell 将：
- 显示*Windows PowerShell 凭据请求*提示你输入凭据的对话框 (*SQL 用户名*和*SQL 密码*) 连接到你的 SQL Server 2017在 Linux 上的实例
- 加载 SQL Server 管理对象 (SMO) 程序集
- 创建的实例[服务器](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.smo.server.aspx)对象
- 连接到**服务器**和显示的几个属性

请记住将**\<your_server_instance\>** 与 IP 地址或你在 Linux 上的 SQL Server 2017 实例的主机名。

```powershell
# Prompt for credentials to login into SQL Server
$serverInstance = "<your_server_instance>"
$credential = Get-Credential

# Load the SMO assembly and create a Server object
[System.Reflection.Assembly]::LoadWithPartialName('Microsoft.SqlServer.SMO') | out-null
$server = New-Object ('Microsoft.SqlServer.Management.Smo.Server') $serverInstance

# Set credentials
$server.ConnectionContext.LoginSecure=$false
$server.ConnectionContext.set_Login($credential.UserName)
$server.ConnectionContext.set_SecurePassword($credential.Password)

# Connect to the Server and get a few properties
$server.Information | Select-Object Edition, HostPlatform, HostDistribution | Format-List
# done
```

PowerShell 应显示类似于下面的输出的信息：

```
Edition          : Developer Edition (64-bit)
HostPlatform     : Linux
HostDistribution : Ubuntu
```
> [!NOTE]
> 如果没有显示这些值的内容，与目标 SQL Server 实例的连接可能已失败。 请确保可以使用相同的连接信息从 SQL Server Management Studio 进行连接。 然后查看[连接故障排除建议](sql-server-linux-troubleshooting-guide.md#connection)。

## <a name="examine-sql-server-error-logs"></a>检查 SQL Server 错误日志

使用 Windows 上的 PowerShell 检查连接到 Linux 上 SQL Server 2017 实例的错误日志。 我们还将使用**Out-gridview** cmdlet 来显示信息从错误日志中的网格视图显示。

复制并粘贴以下命令在 PowerShell 提示符。 它们可能会运行几分钟。 这些命令执行以下操作：
- 显示*Windows PowerShell 凭据请求*提示你输入凭据的对话框 (*SQL 用户名*和*SQL 密码*) 连接到你的 SQL Server 2017在 Linux 上的实例
- 使用**Get SqlErrorLog** cmdlet 来连接到 Linux 上的 SQL Server 2017 实例并检索错误日志以来**昨天**
- 将输出发送到通过管道传递**Out-gridview** cmdlet

请记住将**\<your_server_instance\>** 与 IP 地址或你在 Linux 上的 SQL Server 2017 实例的主机名。

```powershell
# Prompt for credentials to login into SQL Server
$serverInstance = "<your_server_instance>"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday | Out-GridView
# done
```
## <a name="see-also"></a>另请参阅
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
