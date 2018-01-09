---
title: "对 SQL Server 机器学习的升级和安装常见问题解答 |Microsoft 文档"
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 001e66b9-6c3f-41b3-81b7-46541e15f9ea
caps.latest.revision: "59"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 130c52d56e45dae5da5f50ef0d5d96ea87c31d3a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning"></a>对 SQL Server 机器学习的升级和安装常见问题解答

本主题提供有关安装的机器学习中 SQL Server 功能的一些常见问题的答案。 它还介绍有关升级的常见问题。

+ 某些问题只是出现升级从预发行版本。 因此，我们建议你确定你的版本和版本首次在阅读这些说明之前。
+ 升级到最新版本或服务版本越早越好，若要解决在最新版本中修复任何问题。

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务 （数据库）

## <a name="performing-setup-for-the-first-time"></a>第一次执行安装程序

请按照的设置过程[!INCLUDE[sscurrent_md](../../includes/sscurrent_md.md)]和 R 组件，如下所述： 

+ [设置 SQL Server R Services 或机器学习服务数据库中](../r/set-up-sql-server-r-services-in-database.md)
+ [设置 SQL Server 自 2017 年与 Python](../python/setup-python-machine-learning-services.md)
+ [创建独立的 R 服务器](../r/create-a-standalone-r-server.md)

> [!IMPORTANT]
> 
> 安装 SQL Server 和机器学习功能，然后才能使用 R 或 Python 脚本后，你必须完成一些其他配置步骤。 这是因为默认情况下未启用外部脚本执行功能。

### <a name="requirements-and-restrictions"></a>要求和限制

具体取决于要安装的 SQL Server 的版本，以下限制的一些可能适用：

- 在早期版本的 SQL Server 2016 R Services，8.3 文件名表示法已包含的工作目录的驱动器上需要。 如果你安装的预发行版本，则升级到 SQL Server 2016 Service Pack 1 应修复此问题。 此要求不适用于版本后 SP1。

- 目前，无法安装[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]故障转移群集上。 

- 在 Azure VM，可能需要一些额外的配置。 例如，你可能需要创建防火墙例外以支持远程访问。

- 不支持通过并行安装的 R，另一个版本或从 Revolution Analytics，其他版本。

- 不再支持重新安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的任何预发行版本。 如果你使用的预发行版本，则升级越早越好。

- 禁用病毒扫描在开始安装之前。 安装程序完成后，我们建议挂起病毒扫描中使用的文件夹[!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]。 最好是挂起整个上扫描[!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]树。

### <a name="licensing-agreements-for-unattended-installs"></a>对于无人参与安装的许可协议

如果你使用命令行的 SQL Server 实例升级，请确保同时，包含命令行[!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]R 和 Python 的许可协议参数，并使用新的许可证协议参数。

### <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server"></a>脱机安装的 SQL Server 的本地化版本的机器学习组件

当你安装[!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]机学习组件不能访问 internet 的计算机上，你必须执行一些附加步骤：

+ 运行 SQL Server 安装程序之前，R 或 Python 组件安装程序下载到本地文件夹。
+ 在某些情况下，你可能需要编辑的安装程序文件，以确保安装了正确的语言。
+ 用于机器学习组件的语言标识符必须是相同的 SQL Server 安装程序语言，或无法完成安装程序。

有关详细信息，请参阅[安装没有 internet 访问权限的机器学习组件](../r/installing-ml-components-without-internet-access.md)。

## <a name="post-installation-configuration"></a>安装后配置

若要使用 R 或 Python 的机器学习，某些附加配置功能后需要，则运行 SQL Server 安装程序。 所需的精确步骤取决于在服务器和 SQL Server 实例和数据库的配置方式的安全级别。

查看列表中的安装后说明以查看哪些其他的步骤可能需要在你的环境中的所有选项。

+ [设置 SQL Server 机器学习在数据库中](set-up-sql-server-r-services-in-database.md) 

## <a name="upgrades-or-uninstallation"></a>升级或卸载

本部分包含有关特定升级方案的详细的说明。

### <a name="how-to-upgrade-sql-server"></a>如何升级 SQL Server

可以通过重新运行安装程序向导来升级你的 SQL Server 版本。

+ [升级 SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
+ [升级 SQL Server 使用安装向导](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

你可以升级只是机器学习使用称为绑定的进程的组件： 
+ [使用 SqlBindR 升级机学习组件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>停止对从的预发布版本的就地升级的支持

不再支持从 SQL Server 2016 的预发行版本升级。 这包括 SQL Server 2016 CTP3、 CTP3.1、 CTP3.2、 RC0 或 RC1。

以下版本已安装的 SQL Server 2016 的预发行版安装。

| 版本 | 生成         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

如果你怀疑你使用哪个版本方面，运行`@@VERSION`在 SQL Server Management Studio 从查询中。

一般情况下，升级的过程如下所示：

1. 备份脚本和数据。
2. 卸载预发布版本。
3. 安装的发行版。

卸载 SQL Server 的预发行版本机学习组件可能十分复杂，而且可能需要运行特殊的脚本。 请与技术支持联系以获取帮助。

### <a name="support-for-slipstream-upgrades"></a>支持补充升级

补充安装是指对失败的实例安装应用修补或更新，以修复现有的问题。 此方法的优点是，执行安装程序，避免单独重新启动更高版本的同时，将更新为 SQL Server。

如果服务器没有 internet 访问权限，请务必下载 SQL Server 安装程序。 另外，在开始更新过程*之前*，必须单独下载 R 组件安装程序的匹配版本。 

有关下载位置，请参阅[安装没有 internet 访问权限的机器学习组件](installing-ml-components-without-internet-access.md)。

将所有安装文件复制到本地目录后，在命令行中键入 SETUP.EXE 启动安装实用工具。

- 使用*/UPDATESOURCE*自变量以指定包含 SQL Server 更新，如累积更新或 service pack 版本的本地文件的位置。

- 使用*/MRCACHEDIRECTORY*自变量以指定包含的 R 组件 CAB 文件的文件夹。

详细信息，请参阅这篇博客由支持团队：[在没有 internet 访问权限的计算机上部署 R Services](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)。

### <a name="get-machine-learning-components-for-offline-installs"></a>机器学习组件获取脱机安装

如果你安装或升级未连接到 internet 的服务器，你必须下载机器学习组件手动开始刷新之前的更新的版本。 

+ [安装没有 internet 访问权限的机器学习组件](../../advanced-analytics/r/installing-ml-components-without-internet-access.md)。

### <a name="support-policy-and-schedule-for-update-of-machine-learning-components"></a>支持策略和计划的更新的计算机学习组件

发布修补程序或 SQL Server 的改进，机学习组件将被自动升级或刷新，如果你的实例已包括的功能。

截至年 12 月 2016，你可以升级比 SQL Server 版本周期更快的频率的机器学习组件。 通过执行此操作*绑定*现代软件生命周期策略的 SQL Server 实例。 通过机器学习开发团队发布新版本的机器学习工具时，你可以下载最新版本并将其应用到用于机器学习的 SQL Server 实例。

有关详细信息，请参阅：

+ [Microsoft R Server 和机器学习 Server 的支持时间线](https://docs.microsoft.com/machine-learning-server/resources-servicing-support)
+ [使用 SqlBindR 升级的 SQL Server 实例](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

## <a name="r-server-standalone"></a>R Server (Standalone)

本部分介绍特定于安装的 Microsoft R Server （独立版），使用 SQL Server 2016 安装程序问题。 

有关与从 R 服务器到机器学习服务器升级相关的问题，请参阅[安装机器学习用于 Windows 的服务器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)。

### <a name="problems-when-r-services-and-r-server-standalone-are-installed-on-the-same-computer"></a>在同一台计算机上安装 R Services 和 R Server 独立时出现问题

在 SQL Server 2016 的早期版本，有时是同时安装 R Server （独立） 和 R Services （数据库） 导致安装程序失败并显示"拒绝访问"消息。 在 Service Pack 1 中已修复此问题，而且为 SQL Server 2016。

如果你遇到此错误，并且需要升级这些功能，执行带有 SP1 的 SQL Server 2016 的版本补充安装。 有两种方法来解决此问题，这两种需要卸载并重新安装。

1. 卸载 R Services （数据库中），并确保删除 SQLRUserGroup 的用户帐户。

2. 重新启动服务器，并重新安装 R Server （独立）。

3. 运行的 SQL Server 一次设置的详细信息，并这一次选择**向现有 SQL Server 添加功能**。

4. 选择该实例，然后选择**R Services （数据库）**选项以添加。

如果此过程无法解决该问题，请尝试以下解决方法：

1. 在同一时间卸载 R Services （数据库） 和 R Server （独立）。

2. 删除本地用户帐户 (SQLRUserGroup)。

3. 重新启动服务器。

4. 运行 SQL Server 安装程序，并添加 R Services （数据库） 功能仅。 不要选择**R Server （独立）**。

通常情况下，我们建议你不要安装 R Services （数据库） 和 R Server （独立） 在同一台计算机上。 但是，如果服务器具有足够的容量，你可能会发现 R Server 独立可能有用，作为开发工具。 另一种情形是，你需要使用的 R Server 操作化功能，但同时想要访问 SQL Server 数据，而无需数据移动。

## <a name="see-also"></a>另请参阅

 [SQL Server R Services 入门](../r/getting-started-with-sql-server-r-services.md)

 [Microsoft R Server 独立入门](../r/getting-started-with-microsoft-r-server-standalone.md)
