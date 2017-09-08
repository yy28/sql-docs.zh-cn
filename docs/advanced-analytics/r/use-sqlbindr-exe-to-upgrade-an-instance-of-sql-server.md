---
title: "升级 SQL Server 实例中的机器学习组件 |Microsoft 文档"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server (starting with 2016 CTP3)
ms.assetid: 4da80998-f929-4fad-a86f-87d09c1a79ef
caps.latest.revision: 15
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2d9d7ddd95bdbcf6efca98ed94bc305924902b98
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="upgrade-machine-learning-components-in-a-sql-server-instance"></a>升级 SQL Server 实例中的机器学习组件

Microsoft 机器学习用于 Windows 的服务器包括一种工具，你可以使用升级与 SQL Server 的实例关联的 R 组件。 有两个版本的工具： 向导和命令行实用工具。

本文介绍如何使用这些工具来升级兼容的 SQL Server 实例，以及如何将还原先前已升级的实例。

不需要使用此升级过程，如果你想要作为 SQL Server 更新的一部分中获取的升级。 每当你安装新的 service pack 或服务版本，机器学习组件将始终自动升级到最新版本。 如果你想要升级组件以更快的速度比 affored SLQ Server 服务发行版本，只能使用此 proess。

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务

> [!NOTE]
> 在撰写本文时，升级仅适用于兼容的 SQL Server 2016 实例。  尽管升级支持的 SQL Server 自 2017 年，但不已发布用于升级的 Microsoft 机器学习服务器的新版本。

## <a name="upgrade-an-instance"></a>升级实例

升级过程被称为**绑定**，因为它将更改要使用新的现代生命周期策略的 SQL Server 计算机学习组件支持模型。 但是，升级不会更改 SQL Server 数据库的支持模型。

一般情况下，此许可系统可确保数据科学家始终使用 R 的最新版本。有关 Modern Lifecycle 策略的条款的详细信息，请参阅 [Microsoft R Server 的支持时间线](https://msdn.microsoft.com/microsoft-r/rserver-servicing-support)。

绑定实例时，会发生几件事情：

+ 支持模型已更改。 而不是依赖于 SQL Server 服务版本，支持基于新的现代生命周期策略。
+ 机器学习与实例关联的组件将自动升级每个版本中，锁定的步骤是最新的现代生命周期策略下的版本中。 
+ 可能会添加新的 R 或 Python 包。 例如，从 Microsoft R Server 以前的更新添加新的 R 包，如[MicrosoftML](../using-the-microsoftml-package.md)， [olapR](../r/how-to-create-mdx-queries-using-olapr.md)，和[sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md)。
+ 不能再手动更新实例，除非要添加新的包。
+ 你可以选择添加预先训练的模型。

如果你稍后决定你想要停止升级实例中每个版本，则必须**取消绑定**实例中所述[本节](#bkmk_Unbind)，然后卸载机器学习所述的升级这篇文章中：[运行 Microsoft R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)。 过程完成后，将来的机器学习基于学习 Server 计算机上的升级将不再应用到的实例。

### <a name="bkmk_prereqs"></a>升级的先决条件

1. 标识用于升级的候选实例。
    + 已安装了 R Services 的 SQL Server 2016
    + 至少服务包 1 以及 CU3

2. 获取**Microsoft R Server**，通过下载单独的 Windows installer。

    [如何使用独立的 Windows 安装程序在 Windows 上安装 R Server 9.0.1](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#howtoinstall)

> [!TIP]
> 
> 找不到 SqlBindR.exe？ 你可能具有 R Server 尚未下载。 此实用程序时仅使用 Microsoft R Server Windows installer。

### <a name="bkmk_BindWizard"></a>升级使用新的安装向导

1. 启动新的 R Server 安装程序具有你想要升级的实例的计算机上。
  ![Microsoft R Server 安装向导](media/r-server-installer-01.PNG)
2. 接受 Microsoft R Server 9.1.0 的许可协议，然后单击**下一步**。
3. 接受的许可条件对于 R 的开放源组件，然后单击**下一步**。
4. 上**选择安装文件夹**，接受默认值，或指定其他位置将在其中安装 R 库。 
5. 安装程序将标识任何适用于绑定的本地实例。 如果不显示任何实例，则表示未找到任何有效的实例。 你可能需要修补程序服务器，或检查是否已安装 R Services。
6. 选择你想要升级，然后单击任何实例旁边的复选框**下一步**。
7. 过程可能需要一段时间。
    
    在安装期间，SQL Server R Services 使用的 R 库替换库为 Microsoft R Server 9.1.0。
    
    快速启动板不受此过程中，但将删除 R_SERVICES 文件夹中的库和服务的属性将会更改，为使用在库`C:\Program Files\Microsoft\R Server\R_SERVER`。

### <a name="bkmk_BindCmd"></a>升级使用命令行

已安装 Microsoft R Server 后，你可以从命令行运行仅 SqlBindR.exe 工具。

1. 以管理员身份打开命令提示符并导航到包含 sqlbindr.exe 的文件夹。 默认位置是`C:\Program Files\Microsoft\R Server\Setup`
2. 键入以下命令，查看可用实例列表： `SqlBindR.exe /list`
  
   记下所列出的完整实例名称。 例如，实例名称可能是`MSSQL13.MSSQLSERVER`默认实例，或类似`SERVERNAME.MYNAMEDINSTANCE`。
3. 在使用 */bind* 参数的情况下运行 **SqlBindR.exe** 命令，并指定要升级的实例的名称（如上个步骤中所返回）。

   例如，若要升级的默认实例，请键入：`SqlBindR.exe /bind MSSQL13.MSSQLSERVER`
4. 在升级完成后，重新启动与已修改的任何实例关联的启动板服务。


## <a name="bkmk_Unbind"></a>还原或取消绑定实例

若要还原的 SQL Server 以使用 SQL server 安装的原始库实例，必须执行**取消绑定**操作。 你可以执行此操作通过重新运行安装向导的 Microsoft R Server，或通过从命令行运行 SqlBindR 实用程序。

取消绑定时完成，将删除 Microsoft R Server 9.1.0 的库，并还原 SQL Server R Services 使用的原始 R 库。

编辑 SQL Server 快速启动板的属性为使用默认文件夹中的 R 库用于 R_SERVICES， `C:\Program Files\Microsoft\R Server\R_SERVER`。

### <a name="unbind-using-the-wizard"></a>取消绑定使用向导

1. 下载的新安装 Microsoft R Server 9.1.0 程序。
2. 具有你想要取消绑定的实例的计算机上运行安装程序。
2. 安装程序将标识本地实例用于取消绑定的候选。
3. 取消选择你想要还原到原始的 SQL Server R Services 配置实例旁边的复选框。
4. 接受 Microsoft R Server 9.1.0 的许可协议。 即使你要删除 R 服务器，你必须接受许可协议。
5. 单击 **“完成”**。 该进程花费一段时间。

### <a name="unbind-using-the-command-line"></a>取消绑定使用命令行

1. 如上节所述，打开命令提示符并导航到包含 **sqlbindr.exe** 的文件夹。

2. 在使用 */unbind* 参数的情况下运行 **SqlBindR.exe** 命令，并指定实例。

   例如，以下命令将恢复默认实例：
   
    `SqlBindR.exe /unbind MSSQL13.MSSQLSERVER`

## <a name="known-issues"></a>已知问题

本部分列出了已知的问题特定于使用 SqlBindR.exe 实用工具中，或使用 Microsoft R Server 安装程序实用工具的升级，它会影响 SQL Server 实例。

### <a name="restoring-packages-that-were-previously-installed"></a>还原以前安装的程序包

中不包括 Microsoft R Server 9.0.1 升级实用程序，该实用工具不能还原原始包或 R 组件完全，要求用户运行修复的实例上，将应用所有服务版本中，然后重新启动实例。

但是，最新版本的 Microsoft R Server 9.1.0，用于升级实用程序将自动还原原始的 R 功能。 因此，你应该不需要重新安装的 R 组件或重新修补程序服务器。 但是，你仍需要安装任何可能在初始安装后添加的 R 包。

如果已使用包管理角色来安装并共享包，此任务是要容易得多： 你可以使用 R 命令同步到文件系统在数据库中，使用记录的已安装的程序包，反之亦然。 有关详细信息，请参阅[安装和管理 R 包](installing-and-managing-r-packages.md)

### <a name="cannot-perform-upgrade-from-901"></a>无法执行从 9.0.1 升级

如果运行的新安装 Microsoft R Server 9.1.0 程序时，你有以前升级到 9.0.1，SQL Server 2016 R Services 的实例，它将显示所有的有效实例的列表，然后选择默认情况下的以前绑定的实例。 如果继续，则以前绑定的实例是未绑定。 因此，更早版本 9.0.1 删除安装，包括任何相关的包，但未安装 Microsoft R Server (9.1.0) 的新版本。

一种解决方法，您可以修改现有的 R Server 安装，如下所示：
1. 在 Control Panel 中，打开**添加或删除程序**。
2. 找到 Microsoft R Server，并单击**更改/修改**。
3. 安装程序启动时，选择你想要将绑定到 9.1.0 的实例。

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>绑定或取消绑定离开多个临时文件夹

有时也无法清理临时文件夹的绑定和正在取消绑定操作。
如果您发现具有类似名称的文件夹，则可以在安装完成后对其进行删除：`R_SERVICES_<guid>`

> [!NOTE]
> 请务必等待，直到安装已完成。 它可能需要很长时间才能删除关联使用某一版本的 R 库，然后添加新的 R 库。 操作完成后，将删除临时文件夹。

## <a name="sqlbindrexe-command-syntax"></a>sqlbindr.exe 命令语法

### <a name="usage"></a>用法

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>Parameters

|名称|Description|
|------|------|
|*list*| 显示当前计算机上所有 SQL 数据库实例 ID 的列表|
|*bind*| 将指定的 SQL 数据库实例升级至 R Server 最新版本，并确保实例会自动获取 R Server 的未来升级|
|*unbind*|从指定的 SQL 数据库实例中卸载 R Server 最新版本，并防止未来 R Server 升级影响该实例|

### <a name="errors"></a>错误

该工具返回以下错误消息：

|错误|解决方法|
|------|------|
|绑定实例时出错| 无法绑定实例。 请与支持部门联系获取帮助。|
|实例已绑定| 已运行 *bind* 命令，但指定的实例已绑定。 选择其他实例。|
|实例未绑定| 已运行 *unbind* 命令，但指定的实例未绑定。 选择一个兼容的不同实例。|
|不是有效的 SQL 实例 ID| 键入的实例名称可能不正确。 使用 *list* 参数再次运行该命令，查看可用的实例 ID。|
|未找到任何实例| 此计算机不具有 SQL Server R Services 的实例。|
|实例必须已安装 SQL R Services（数据库内）的兼容版本。| 有关详细信息，请参阅本主题中的兼容性要求。|
|取消绑定实例时出错| 无法取消绑定实例。 请与支持部门联系获取帮助。|
|发生意外错误| 其他错误。 请与支持部门联系获取帮助。  |
|未找到任何 SQL 实例| 此计算机不具有 SQL Server 的实例。 |

有关详细信息，请参阅 Microsoft R server 的发行说明：

+ [什么是 R Server 中的新增功能](https://docs.microsoft.com/r-server/whats-new-in-r-server)

+ [R Server 的已知问题](https://docs.microsoft.com/r-server/resources-known-issues)

