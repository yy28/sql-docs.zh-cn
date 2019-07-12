---
title: 管理使用 PowerShell 在 Linux 上的 SQL Server
description: 本文提供使用 PowerShell 在 Linux 上的 SQL Server 与 Windows 上的概述。
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: a3492ce1-5d55-4505-983c-d6da8d1a94ad
ms.openlocfilehash: 21ce61a823281c5e6688bcfb8aee96d296cb671d
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834934"
---
# <a name="use-powershell-on-windows-to-manage-sql-server-on-linux"></a>使用 Windows 上的 PowerShell 管理 Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍了[SQL Server PowerShell](../powershell/sql-server-powershell.md)并指导你完成几个示例如何将用于在 Linux 上的 SQL Server。 SQL Server 的 PowerShell 支持目前在 Windows、 MacOS 和 Linux 上。 本文介绍如何使用 Windows 计算机连接到 Linux 上的远程 SQL Server 实例。

## <a name="install-the-newest-version-of-sql-powershell-on-windows"></a>在 Windows 上安装最新版本的 SQL PowerShell

[SQL PowerShell](../powershell/download-sql-server-ps-module.md)在 Windows 上维护 PowerShell 库中。 当使用 SQL Server 时，应始终使用 SqlServer PowerShell 模块的最新版本。

## <a name="before-you-begin"></a>开始之前

读取[已知问题](sql-server-linux-release-notes.md)Linux 上的 SQL Server。

## <a name="launch-powershell-and-import-the-sqlserver-module"></a>启动 PowerShell 并导入*sqlserver*模块

首先在 Windows 上启动 PowerShell。 使用<kbd>赢得</kbd>+<kbd>R</kbd>，在您的 Windows 计算机，然后键入**PowerShell**以启动新的 Windows PowerShell 会话。

```
PowerShell
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

让我们使用 PowerShell 在 Windows 上连接到 Linux 上的 SQL Server 实例，并显示几个服务器属性。

复制并粘贴以下命令在 PowerShell 提示符下。 运行这些命令时，PowerShell 将：
- 显示一个对话框，提示您输入的主机名或实例的 IP 地址
- 显示*Windows PowerShell 凭据请求*对话框，提示你输入凭据。 可以使用你*SQL 用户名*并*SQL 密码*连接到 Linux 上的 SQL Server 实例
- 使用**Get SqlInstance** cmdlet 连接到**Server**并显示几个属性

（可选） 您只需替换`$serverInstance`变量与 IP 地址或主机名的 SQL Server 实例。

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Connect to the Server and get a few properties
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

用于连接到 SQL Server 实例的另一个选项是使用[SQL Server PowerShell 提供程序](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider)。  此提供程序可用于导航像您已在对象资源管理器，但命令行在树结构中导航到类似的 SQL Server 实例。  默认情况下此提供程序显示为名为 PSDrive`SQLSERVER:\`可以用于连接和导航您的域帐户有权的 SQL Server 实例。  请参阅[配置步骤](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-auth-overview#configuration-steps)有关如何安装 Linux 上的 SQL Server 的 Active Directory 身份验证的信息。

此外可以使用 SQL Server PowerShell 提供程序使用 SQL 身份验证。 若要执行此操作，请使用`New-PSDrive`cmdlet 来创建新的 PSDrive，提供正确的凭据才能连接。

在此示例中，您将看到如何创建新的 PSDrive 使用 SQL 身份验证的一个示例。

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

下面是输出可能如下所示。  您可能注意到输出结果类似于 SSMS 将显示在数据库节点。  它将显示用户数据库，但不是系统数据库。

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

如果你需要查看您的实例上的所有数据库，一种方法是使用[Get-sqldatabase](https://docs.microsoft.com/powershell/module/sqlserver/Get-SqlDatabase) cmdlet。

## <a name="examine-sql-server-error-logs"></a>检查 SQL Server 错误日志

以下步骤在 Windows 上使用 PowerShell 检查连接 Linux 上的 SQL Server 实例的日志的错误。 我们还将使用**Out-gridview** cmdlet 来显示信息的错误日志中的网格视图显示。

复制并粘贴以下命令在 PowerShell 提示符下。 它们可能会运行几分钟。 这些命令执行以下操作：
- 显示一个对话框，提示您输入的主机名或实例的 IP 地址
- 显示*Windows PowerShell 凭据请求*对话框，提示你输入凭据。 可以使用你*SQL 用户名*并*SQL 密码*连接到 Linux 上的 SQL Server 实例
- 使用**Get-sqlerrorlog** cmdlet 来连接到 Linux 上的 SQL Server 实例并检索错误日志以来**昨天**
- 通过管道传递到输出**Out-gridview** cmdlet

（可选） 可以替换`$serverInstance`变量与 IP 地址或主机名的 SQL Server 实例。

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday | Out-GridView
# done
```
## <a name="see-also"></a>请参阅
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
- [SqlServer cmdlet](https://docs.microsoft.com/powershell/module/sqlserver)
