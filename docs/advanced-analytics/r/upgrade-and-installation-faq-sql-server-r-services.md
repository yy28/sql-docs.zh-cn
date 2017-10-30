---
title: "升级和安装常见问题解答 (SQL Server R Services) |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 001e66b9-6c3f-41b3-81b7-46541e15f9ea
caps.latest.revision: 59
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: 395554af6b9d014d560d8b6520d032966630c5b2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/08/2017

---
# <a name="upgrade-and-installation-faq-sql-server-r-services"></a>升级和安装常见问题解答 (SQL Server R Services)

本主题提供有关安装的机器学习中 SQL Server 功能的一些常见问题的答案。 它还介绍有关升级的常见问题。 某些问题只是出现升级从预发行版本。 因此，我们建议尽可能快地识别你的版本和版本第一个，然后升级到最新版本或服务版本。

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务 （数据库）

## <a name="performing-setup-for-the-first-time"></a>第一次执行安装程序

请按照的设置过程 [！INCLUDEssCurrent] 和 R 组件，如下所述： 

+ [设置 SQL Server R Services 或机器学习服务数据库中](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)
+ [设置 SQL Server 自 2017 年与 Python](../python/setup-python-machine-learning-services.md)
+ [创建 R Server（独立版）](create-a-standalone-r-server.md)

已安装 SQL Server，以使用外部 R 或 Python 脚本之后, 你必须完成一些额外的配置。 这是因为默认情况下未启用外部脚本执行功能。

> [!NOTE]
> 请勿使用在公开发布的 SQL Server 2016 的版本之前发布的设置说明。 安装过程早期发行版本和正式发行版本之间完全更改。 

### <a name="requirements-and-restrictions"></a>要求和限制

具体取决于要安装的 R Services 的版本，以下限制的一些可能适用：

- 在早期版本的 SQL Server 2016 R Services，8.3 文件名表示法已包含的工作目录的驱动器上需要。 如果你安装的预发行版本，但如果升级到 SQL Server 2016 Service Pack 1，则应删除此要求。

- 不能在故障转移群集上安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 。 

- 在 Azure VM，可能需要一些额外的配置。 例如，你可能需要创建防火墙例外以支持远程访问。

- 不支持通过并行安装的 R，另一个版本或从 Revolution Analytics，其他版本。

- 不再支持重新安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的任何预发行版本。 如果你使用的预发行版本，则升级越早越好。

- 禁用病毒扫描在开始安装之前。 安装程序完成后，我们建议挂起病毒扫描上使用 SQL Server （最好是整个树） 的文件夹。

### <a name="licensing-agreements-for-unattended-installs"></a>对于无人参与安装的许可协议

如果你使用命令行的 SQL Server 实例升级，请确保命令行包含新的许可证协议参数， */IACCEPTROPENLICENSEAGREEMENT*。 如果不使用此参数，安装程序可能会失败。

### <a name="offline-installation-of-r-components-for-a-localized-version-of-sql-server"></a>脱机安装的 SQL Server 的本地化版本的 R 组件

在没有 internet 访问的计算机上安装 R Services 时，你必须执行两个其他步骤。 在运行 SQL Server 安装程序，并编辑安装程序文件，以确保安装了正确的语言之前，R 组件安装程序下载到本地文件夹。

用于的 R 组件的语言标识符必须是 SQL Server 安装程序语言中，与相同或**下一步**按钮处于禁用状态，无法完成安装程序。

有关详细信息，请参阅[Installing R Components without internet 访问](../../advanced-analytics/r-services/installing-ml-components-without-internet-access.md)。

## <a name="post-installation-configuration"></a>安装后配置

若要使用 R 或 Python 的机器学习，某些附加配置功能后需要，则运行 SQL Server 安装程序。 具体取决于安全级别的服务器和 SQL Server 实例和数据库的可能需要使用其他步骤。 查看从以确定任何其他配置可能需要的设置说明这些步骤。

[设置 SQL Server R Services 中的数据库](set-up-sql-server-r-services-in-database.md)

- 支持运行外部脚本，如 R 或 Python，该功能默认情况下，数据库安全性处于禁用状态，并必须启用。

- 确保快速启动板用于运行 R 或 Python 的辅助帐户有权访问该实例。

- 你可能需要启用远程访问在服务器上，或创建允许与 SQL Server 的入站的通信的防火墙规则。

- 根据计划的工作负荷，你可能需要优化机器学习任务的服务器。 

## <a name="upgrades-or-uninstallation"></a>升级或卸载

本部分包含有关特定升级方案的详细的说明。

不再支持从 SQL Server 2016 R Services 的预发行版本升级。 我们建议您卸载预发布版本中，，，然后尽快安装发行版本。

### <a name="support-for-slipstream-upgrades"></a>支持补充升级

补充安装是指对失败的实例安装应用修补或更新，以修复现有的问题。 此方法的优点是，执行安装程序，避免单独重新启动更高版本的同时，将更新为 SQL Server。

如果服务器没有 internet 访问权限，请务必下载 SQL Server 安装程序。 另外，在开始更新过程*之前*，必须单独下载 R 组件安装程序的匹配版本。 

有关下载位置，请参阅[没有 internet 访问权限的安装 R 组件](installing-ml-components-without-internet-access.md)。

将所有安装文件复制到本地目录后，在命令行中键入 SETUP.EXE 启动安装实用工具。

- 使用*/UPDATESOURCE*自变量以指定包含 SQL Server 更新，如累积更新或 service pack 版本的本地文件的位置。

- 使用*/MRCACHEDIRECTORY*自变量以指定包含的 R 组件 CAB 文件的文件夹。

详细信息，请参阅这篇博客由支持团队：[在没有 internet 访问权限的计算机上部署 R Services](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)。

### <a name="upgrade-r-components-offline"></a>升级脱机 R 组件

如果你安装或升级未连接到 internet 的服务器，必须在开始刷新之前手动下载的 R 组件的更新的版本。 有关详细信息，请参阅[没有 internet 访问权限的安装 R 组件](../../advanced-analytics/r-services/installing-ml-components-without-internet-access.md)。

### <a name="schedule-for-update-of-r-components"></a>计划的 R 组件的更新

发布修补程序或 SQL Server 2016 的改进，R 组件还升级或刷新，如果你的实例已经包含了 R 服务功能。

如果你使用的 SQL Server 自 2017 年，将自动安装升级到 R 组件。

截至年 12 月 2016，你可以升级比 SQL Server 版本周期更快的频率的 R 组件。 通过执行此操作*绑定*现代软件生命周期策略 R Services 的实例。 当前仅对升级 2016年实例提供支持。 当发布新版本的 R Server 后时，你将能够升级到以及 2017年实例。

有关详细信息，请参阅[使用 SqlBindR 升级的 SQL Server R Services 实例](../../advanced-analytics/r-services/use-sqlbindr-exe-to-upgrade-an-instance-of-r-services.md)。

### <a name="upgrade-from-a-pre-release-version-of-sql-server-2016"></a>从 SQL Server 2016 的预发行版本升级

一般情况下，为所有预发行版本不支持的就地升级。

若要成功安装 R Services，你必须卸载任何早期版本的[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]及其相关的 R 组件。 这包括 SQL Server 2016 CTP3、 CTP3.1、 CTP3.2、 RC0 或 RC1。

卸载预发布版本，可以十分复杂，而且需要运行一个特殊的脚本。 请与技术支持联系以获取帮助。

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

如果你怀疑你使用哪个版本方面，运行`@@VERSION`从 SQL Server Management Studio。

### <a name="problems-with-setup-of-r-server-standalone"></a>R Server （独立版） 的安装程序出现问题

本部分介绍特定于安装的 Microsoft R Server （独立版），使用 SQL Server 2016 安装程序问题。 有关与 R Server 升级相关的更多常规问题，请参阅[Microsoft R Server](https://msdn.microsoft.com/microsoft-r/) MSDN 上。

#### <a name="failure-to-install-localized-versions"></a>未能安装本地化的版本

在脱机安装 R Server 时，预发行版本不允许你使用本地化的语言。

通常情况下，如果服务器不具有 internet 访问权限，运行安装程序之前必须安装的所有包为都下载 R Server。 然后在安装期间指定的文件的位置。

但是，如果安装程序包与关联的语言标识符不是 SQL Server 安装程序语言相同，则出现问题。 当你达到 R 组件安装的页时**下一步**按钮处于禁用状态，因此无法继续安装。 一种解决方法，你可以重命名包以使用匹配的标识符。

例如，安装包的名称可能`SRO_3.2.2.0_1031.cab`。
若要在 SQL Server 上安装的 104 语言，文件重命名为`SRO_3.2.2.0_1041.cab`。

#### <a name="installing-r-services-and-r-server-standalone-on-the-same-computer"></a>在同一台计算机上安装 R Services 和 R Server 独立

通常情况下，你并不安装 R Services （数据库） 和 R Server （独立） 在同一台计算机上。 但是，如果服务器具有足够的容量，R Server 独立可能会有用作为开发工具。 你可能还需要使用 R Server 操作化功能，并从 R 服务器访问 SQL Server 数据，而无需数据移动。

请注意，是否同一台计算机上安装 R Server 和 R 服务，将安装两个单独的相同的 R 库集。 一个是以供 SQL Server 实例中，使用，一个是用于部署使用，也使用 R Server。

在 SQL Server 2016 的早期版本，在同一时间安装 R Server （独立） 和 R Services （数据库） 可能会导致安装程序失败并显示"拒绝访问"消息。 在 Service Pack 1 中已修复此问题，而且为 SQL Server 2016。

如果你遇到此错误，并且需要升级这些功能，执行带有 SP1 的 SQL Server 2016 的版本补充安装。 有两种方法来解决此问题，这两种需要卸载并重新安装。

1. 卸载 R Services （数据库中），并确保删除 SQLRUserGroup 的用户帐户。

2. 重新启动服务器，并重新安装 R Server （独立）。

3. 运行的 SQL Server 一次设置的详细信息，并这一次选择**向现有 SQL Server 添加功能**。

4. 选择该实例，然后选择**R Services （数据库）**选项以添加。

在某些情况下，此过程将失败来解决该问题。 请尝试以下解决方法：

1. 在同一时间卸载 R Services （数据库） 和 R Server （独立）。

2. 删除本地用户帐户 (SQLRUserGroup)。

3. 重新启动服务器。

4. 运行 SQL Server 安装程序，并添加 R Services （数据库） 功能仅。 不要选择**R Server （独立）**。

## <a name="see-also"></a>另请参阅

 [SQL Server R Services 入门](../r/getting-started-with-sql-server-r-services.md)

 [Microsoft R Server 独立入门](../r/getting-started-with-microsoft-r-server-standalone.md)

