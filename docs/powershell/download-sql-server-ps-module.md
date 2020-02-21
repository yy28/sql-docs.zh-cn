---
title: 下载 SQL Server PowerShell 模块
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: carlrab
ms.custom: ''
ms.date: 01/23/2020
ms.openlocfilehash: 99976a12ae76254da5b50c5467df9d9e42fdbbce
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "76920350"
---
# <a name="install-the-sql-server-powershell-module"></a>安装 SQL Server PowerShell 模块

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

本文提供安装 SqlServer  PowerShell 模块的指导。

## <a name="powershell-modules-for-sql-server"></a>适用于 SQL Server 的 PowerShell 模块

提供两种 SQL Server PowerShell 模块：

- **SqlServer**：SqlServer 模块包括新的 cmdlet，用于支持最新的 SQL 功能。 该模块还包含 SQLPS 中 cmdlet 的更新版本  。 若要下载 SqlServer 模块，请[在 PowerShell 库中转到 SqlServer 模块](https://www.powershellgallery.com/packages/Sqlserver)。
- **SQLPS**：虽然 SQL Server 安装附带了 SQLPS 模块（用于向后兼容），但该模块不再更新。 最新的 PowerShell 模块是 SqlServer 模块  。

> [!NOTE]
> PowerShell 库中这些版本的 SqlServer  模块支持版本控制并且要求 PowerShell 5.0 或更高版本。

有关帮助主题，请转到：

- [SqlServer](https://docs.microsoft.com/powershell/module/sqlserver) cmdlet。
- [SQLPS](https://docs.microsoft.com/powershell/module/sqlps) cmdlets。

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

从版本 17.0 开始，SQL Server Management Studio (SSMS) 不会安装任何 PowerShell 模块。 要在 SSMS 中使用 PowerShell，则必须从 [PowerShell 库](https://www.powershellgallery.com/packages/Sqlserver)安装 SqlServer  模块。

> [!NOTE]
> 对于 16.x 版本的 SSMS，SQL Server Management Studio (SSMS) 中包含早期版本的 SqlServer  模块

## <a name="azure-data-studio"></a>Azure Data Studio

Azure Data Studio 不会安装任何一个 PowerShell 模块。 若要将 PowerShell 与 Azure Data Studio 一起使用，请从 [PowerShell 库](https://www.powershellgallery.com/packages/Sqlserver)安装 SqlServer  模块。

可以使用 [PowerShell 扩展](../azure-data-studio/powershell-extension.md)，此扩展在 Azure Data Studio 中提供丰富的 PowerShell 编辑器支持。

## <a name="installing-or-updating-the-sqlserver-module"></a>安装或更新 SqlServer 模块

要从 PowerShell 库安装 SqlServer  模块，请以管理员身份启用 [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting) 会话。 还可以以管理员身份启动 Azure Data Studio，并在集成终端的 PowerShell 会话中运行这些命令。

### <a name="install-the-sqlserver-module"></a>安装 SqlServer 模块

在 PowerShell 会话中运行以下命令，为所有用户安装 SqlServer 模块：

```powershell
Install-Module -Name SqlServer
```

### <a name="to-view-the-versions-of-the-sqlserver-module-installed"></a>查看已安装的 SqlServer 模块的版本

执行以下命令来查看已安装的 SqlServer 模块的版本

```powershell
Get-Module SqlServer -ListAvailable
```

### <a name="install-for-the-current-user-rather-than-as-an-administrator"></a>为当前用户而不是以管理员身份安装

如果不能以管理员身份运行 PowerShell 会话，则使用以下命令为当前用户安装：

```powershell
Install-Module -Name SqlServer -Scope CurrentUser
```

### <a name="to-overwrite-a-previous-version-of-the-sqlserver-module"></a>覆盖先前版本的 SqlServer 模块

还可以使用 `Install-Module` 命令覆盖以前的版本。

```powershell
Install-Module -Name SqlServer -AllowClobber
```

> [!Note]
> PowerShell 始终使用安装的最新模块。

### <a name="update-the-installed-version-of-the-sqlserver-module"></a>更新 SqlServer 模块的安装版本

当 SqlServer  模块的更新版本可用时，可使用以下命令安装更新版本：

```powershell
Install-Module -Name SqlServer -AllowClobber
```

可以使用 `Update-Module` 命令安装最新版本的 SQLServer PowerShell 模块，但这不会删除旧版本。 它将并行安装更新版本，以使你能够体验最新版本，但仍会安装旧模块。

但是，如果不想保留旧模块版本，可以使用 `Uninstall-Module` 命令删除以前的版本。

如果安装了多个版本，则可以使用以下命令列出：

```powershell
Get-Module SqlServer -ListAvailable
```

使用以下命令删除旧版本：

```powershell
Uninstall-module -Name SQLServer -RequiredVersion "<version number>" -AllowClobber
```

### <a name="troubleshooting"></a>故障排除

如果在安装过程中出现问题，请参阅[安装模块文档](https://www.powershellgallery.com/packages/PowerShellGet/2.2.1)和[安装模块参考](https://docs.microsoft.com/powershell/module/powershellget/Install-Module)。

## <a name="using-a-specific-version-of-the-sqlserver-module"></a>使用 SqlServer 模块的特定版本

要使用特定版本的模块，请使用类似以下命令的特定版本号将其导入：

```powershell
Import-Module SqlServer -Version 21.1.18080
```

## <a name="pre-release-versions-of-the-sqlserver-module"></a>SqlServer 模块的预发行版本

PowerShell 库中可能提供 SqlServer 模块的预发行（或“预览”）版本。

> [!IMPORTANT]
> 可通过传递 -AllowPrerelease 切换，使用更新后的 Find-Module 和 Install-Module cmdlet（属于 [PowerShellGet](https://www.powershellgallery.com/packages/PowerShellGet) 模块）找到并安装这些版本。    若要使用这些 cmdlet，请安装 PowerShellGet 模块，然后打开一个新的会话。

### <a name="to-discover-pre-release-versions-of-the-sqlserver-module"></a>发现 SqlServer 模块的预发行版本

若要找到 SqlServer 模块的预发行（预览）版本，可运行以下命令：

```powershell
Find-Module SqlServer -AllowPrerelease
```

### <a name="to-install-a-specific-pre-release-version-of-the-sqlserver-module"></a>安装 SqlServer 模块的特定预发行版本

若要安装模块的特定预发行版本，请使用特定版本号安装该模块。

可以尝试使用以下命令：

```powershell
Install-Module SqlServer -RequiredVersion 21.1.18040-preview -AllowPrerelease
```

## <a name="sql-server-powershell-on-linux"></a>Linux 上的 SQL Server PowerShell

若要了解如何在 Linux 上安装 SQL Server PowerShell，请访问[通过 PowerShell Core 管理 Linux 上的 SQL Server](../linux/sql-server-linux-manage-powershell-core.md)。
