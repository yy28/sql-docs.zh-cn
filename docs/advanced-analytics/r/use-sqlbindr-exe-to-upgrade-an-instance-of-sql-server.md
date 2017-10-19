---
title: "升级 SQL Server 实例中的机器学习组件 |Microsoft 文档"
ms.custom: 
ms.date: 10/11/2017
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
ms.sourcegitcommit: 560965a241b24a09f50a23faf63ce74d0049d5a7
ms.openlocfilehash: 9b2d59d860d72207b196ac60a1db66f09baa1228
ms.contentlocale: zh-cn
ms.lasthandoff: 10/13/2017

---
# <a name="upgrade-machine-learning-components-in-a-sql-server-instance"></a>升级 SQL Server 实例中的机器学习组件

本文介绍的过程_绑定_，可以用于升级机器学习在 SQL Server 中使用的组件。 绑定的过程将锁定服务器到基于机器学习服务器而不是 SQL Server 的版本更新频率。

> [!IMPORTANT]
> 不需要使用此升级过程，如果你想要作为 SQL Server 更新的一部分中获取的升级。 每当你安装新的 service pack 或服务版本，机器学习组件将始终自动升级到最新版本。 如果你想要升级以更快的速度比 SQL Server 服务版本提供的组件，请使用此过程。

如果在任何你想要停止在机器学习服务器计划的升级的时，你必须_取消绑定_实例中所述[本节](#bkmk_Unbind)，卸载机器学习服务器。

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务

## <a name="binding-vs-upgrading"></a>与升级的绑定

升级机器学习组件的过程中被称为**绑定**，因为它将更改要使用新的现代软件生命周期策略的 SQL Server 计算机学习组件支持模型。 

一般情况下，切换到新的授权模型可确保数据科学家可以始终使用最新版本的 R 或 Python。 有关现代的生命周期策略的条款的详细信息，请参阅[Microsoft R Server 的支持时间线](https://msdn.microsoft.com/microsoft-r/rserver-servicing-support)。

> [!NOTE]
> 升级不会更改 SQL Server 数据库的支持模型，并不会更改 SQL Server 的版本。

当你将绑定实例时，将发生下列情况，其中包括升级到机器学习组件：

+ 支持模型已更改。 而不是依赖于 SQL Server 服务版本，支持基于新的现代生命周期策略。
+ 自动升级与实例相关联的机器学习组件，每个版本中，锁定的步骤是最新的现代生命周期策略下的版本中。 
+ 可能会添加新的 R 或 Python 包。 例如，从 Microsoft R Server 以前的更新添加新的 R 包，如[MicrosoftML](../using-the-microsoftml-package.md)， [olapR](../r/how-to-create-mdx-queries-using-olapr.md)，和[sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md)。
+ 不能再手动更新实例，除非要添加新的包。
+ 你可以添加预先训练的模型由 Microsoft 提供的选项。

## <a name="bkmk_prereqs"></a>Prerequisites

首先确定要升级的候选的实例。 如果你运行安装程序，并选择绑定选项，则返回与升级兼容的实例的列表。 

请参阅下表获取受支持的升级和要求的列表。

| SQL Server 版本| 支持的升级| 说明|
|-----|-----|------|
| SQL Server 2016| 机器学习服务器 9.2.1| 至少需要 Service Pack 1 加上 CU3。 必须安装并启用 R Services。|
| SQL Server 2017| 机器学习服务器 9.2.1| 必须安装并启用机器学习服务 （数据库）。 |

## <a name="bind-or-upgrade-an-instance"></a>将绑定或升级实例

Microsoft 机器学习用于 Windows 的服务器包含一个可用于升级机器学习语言和工具与 SQL Server 的实例关联的工具。 有两个版本的工具： 向导和命令行实用工具。

在可以运行向导或命令行工具之前，必须下载机器学习组件的独立安装的最新版本。

+ [安装机器学习适用于 Windows Server 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)

+ [下载所需的脱机安装组件](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)

### <a name="bkmk_BindWizard"></a>升级使用新的安装向导

1. 启动新计算机学习服务器安装程序。 请确保具有你想要升级的实例的计算机上运行安装程序。

    ![Microsoft 机器学习 Server 安装向导](media/mls-921-installer-start.PNG)

2. 在页上，**配置安装**，确认要升级的组件，并查看兼容的实例的列表。 如果未不显示任何实例，请检查[先决条件](#bkmk_prereqs)。

    若要升级的实例，请选择实例名称旁边的复选框。 如果不选择实例，将创建机器学习 Server 的单独安装，并且 SQL Server 库保持不变。

    ![Microsoft 机器学习 Server 安装向导](media/configure-the-installation.PNG)

3. 上**许可协议**页上，选择**我接受这些条款**机器学习服务器接受许可条款。 

4. 在后续页上，提供以选择，如 Microsoft R Open 或 Python Anaconda 分发任何开放源组件的其他许可条件的同意。

5. 上**几乎存在**页上，记下的安装文件夹。 默认文件夹是`~\Program Files\Microsoft\ML Server`。 

    如果你想要更改安装文件夹，请单击**高级**以返回到向导的第一页。 但是，你必须重复所有以前的选择。 

6. 如果你要安装的组件脱机，你可能会提示您为所需的计算机学习组件，如 Microsoft R Open、 Python 服务器和 Python 打开的位置。
    
在安装期间，会替换 SQL Server 使用的任何 R 或 Python 库和快速启动板更新为使用较新的组件。 也就是说，如果实例以前使用的默认 R_SERVICES 文件夹中的库，升级后这些库会移除并且快速启动板服务的属性发生更改，以在你指定的位置使用的库。

### <a name="bkmk_BindCmd"></a>升级使用命令行

如果你不希望使用向导，你可以安装机器学习服务器，然后 SqlBindR.exe 工具从命令行运行以升级实例。

> [!TIP]
> 
> 找不到 SqlBindR.exe？ 你可能尚未下载上面列出的组件。 此实用程序时仅使用 Windows installer 机器学习服务器。

1. 以管理员身份打开命令提示符并导航到包含 sqlbindr.exe 的文件夹。 默认位置是`C:\Program Files\Microsoft\MLServer\Setup`

2. 键入以下命令，查看可用实例列表： `SqlBindR.exe /list`
  
   记下所列出的完整实例名称。 例如，实例名称可能是`MSSQL14.MSSQLSERVER`默认实例，或类似`SERVERNAME.MYNAMEDINSTANCE`。

3. 运行**SqlBindR.exe**命令*/绑定*自变量，并指定要升级，实例的名称使用上一步中返回的实例名称。

   例如，若要升级的默认实例，请键入：`SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. 完成升级后，重新启动任何实例已修改与关联的快速启动板服务。

## <a name="bkmk_Unbind"></a>还原或取消绑定实例

如果你决定不再想要升级机器学习使用机器学习服务器组件，你必须首先_取消绑定_实例，然后卸载机器学习的服务器。

+ 取消绑定实例

    你可以取消绑定实例化并还原为使用这两种方法之一来安装 SQL server 的原始库：

    + [使用安装向导](#bkmk_wizunbind)对于机器学习服务器，然后取消选择该实例上的所有功能
    + [使用 SqlBindR 实用工具](#bkmk_cmdunbind)与`/unbind`自变量，后面加上实例名称。

    正在取消绑定过程完成后，将来的机器学习基于学习 Server 计算机上的升级将不再应用到的实例。

+ 卸载机器学习服务器

    有关说明，请参阅[卸载机器学习用于 Windows 的服务器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-uninstall)。 

### <a name="bkmk_wizunbind"></a>取消绑定使用向导

1. 找到的安装程序机器学习服务器。 如果你已删除安装程序，你可能需要再次下载或将其复制从另一台计算机。
2. 请确保具有你想要取消绑定的实例的计算机上运行安装程序。
2. 安装程序会标识适用于取消绑定的候选项的本地实例。
3. 取消选择你想要还原到原始配置实例旁边的复选框。
4. 接受许可协议。 在安装时，必须指示你接受许可条款偶数。
5. 单击 **“完成”**。 该进程花费一段时间。

### <a name="bkmk_cmdunbind"></a>取消绑定使用命令行

1. 如上节所述，打开命令提示符并导航到包含 **sqlbindr.exe** 的文件夹。

2. 在使用 */unbind* 参数的情况下运行 **SqlBindR.exe** 命令，并指定实例。

   例如，以下命令将恢复默认实例：
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

## <a name="known-issues"></a>已知问题

本部分列出了已知的问题特定于使用 SqlBindR.exe 实用工具中，或可能会影响 SQL Server 实例的计算机学习服务器的升级。

### <a name="restoring-packages-that-were-previously-installed"></a>还原以前安装的程序包

中不包括 Microsoft R Server 9.0.1 升级实用程序，该实用工具不能还原原始包或 R 组件完全，要求用户运行修复的实例上，将应用所有服务版本中，然后重新启动实例。

但是，升级实用程序的最新版本会自动还原原始的 R 功能。 因此，你应该不需要重新安装的 R 组件或重新修补程序服务器。 但是，你必须安装可能在初始安装后添加任何 R 包。

如果已使用包管理角色来安装并共享包，此任务是要容易得多： 你可以使用 R 命令同步到文件系统在数据库中，使用记录的已安装的程序包，反之亦然。 有关详细信息，请参阅[for SQL Server 的 R 包管理](r-package-management-for-sql-server-r-services.md)。

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>从 SQL Server 的多个升级的问题

如果运行的新安装 Microsoft R Server 9.1.0 程序时，你有以前升级到 9.0.1，SQL Server 2016 R Services 的实例，它将显示所有的有效实例的列表，然后默认情况下，选择以前绑定的实例。 如果继续，则以前绑定的实例是未绑定。 因此，更早版本 9.0.1 删除安装，包括任何相关的包，但未安装 Microsoft R Server (9.1.0) 的新版本。

一种解决方法，您可以修改现有的 R Server 安装，如下所示：
1. 在 Control Panel 中，打开**添加或删除程序**。
2. 找到 Microsoft R Server，并单击**更改/修改**。
3. 安装程序启动时，选择你想要将绑定到 9.1.0 的实例。

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>绑定或取消绑定离开多个临时文件夹

有时也无法清理临时文件夹的绑定和正在取消绑定操作。
如果您发现具有类似名称的文件夹，则可以在安装完成后对其进行删除：`R_SERVICES_<guid>`

> [!NOTE]
> 请务必等待，直到安装已完成。 它可能需要很长时间才能删除关联使用某一版本的 R 库，然后添加新的 R 库。 操作完成后，会删除临时文件夹。

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

+ [机器学习 Server 中的已知的问题](https://docs.microsoft.com/machine-learning-server/resources-known-issues)

+ [从以前的版本中的 R Server 的功能公告](https://docs.microsoft.com/r-server/whats-new-in-r-server)

+ [已弃用，不再使用或更改的特性](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
