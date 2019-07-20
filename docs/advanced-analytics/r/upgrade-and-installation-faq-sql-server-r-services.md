---
title: 升级和安装常见问题 (FAQ)
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
ms.author: davidph
author: dphansen
ms.openlocfilehash: 71a6149f1d89a4a1df114f376c250c203a8721cf
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344908"
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>SQL Server 机器学习或 R Server 的升级和安装常见问题解答
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本主题提供有关在 SQL Server 中安装机器学习功能的一些常见问题的解答。 还介绍了有关升级的常见问题。

+ 某些问题仅适用于从预发布版本进行升级。 因此, 建议你在阅读这些说明之前先确定版本和版本。 若要获取版本信息, `@@VERSION`请在 SQL Server Management Studio 中的查询中运行。
+ 尽快升级到最新版本或服务版本, 以解决在最新版本中修复的任何问题。

**适用范围：** SQL Server 2016 R Services SQL Server 2017 机器学习服务 (数据库内)

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>SQL Server 2016 的旧版本的要求和限制 

根据要安装 SQL Server 的版本, 可能会出现以下限制:

- 在早期版本的 SQL Server 2016 R Services 中, 在包含工作目录的驱动器上需要8dot3 表示法。 如果你安装了预发行版本, 则升级到 SQL Server 2016 Service Pack 1 应可以解决此问题。 此要求不适用于 SP1 之后的版本。

- 目前不能在故障[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]转移群集上安装。 但是, 如果想要在测试环境中评估此功能, SQL Server 2019 preview 提供故障转移支持。 有关详细信息, 请参阅[新增功能](../what-s-new-in-sql-server-machine-learning-services.md)。

- 在 Azure VM 上, 可能需要进行一些其他配置。 例如, 你可能需要创建防火墙例外以支持远程访问。

- 不支持使用其他版本的 R 或与革命 Analytics 中的其他版本进行并行安装。

- 开始安装之前, 请禁用病毒扫描。 安装完成后, 建议在使用[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]的文件夹上挂起病毒扫描。 最好在整个[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]树上挂起扫描。

 - 在 Windows Core 上安装 SQL Server 的实例上安装 Microsoft R Server。 在 SQL Server 2016 的 RTM 版本中, 将 Microsoft R Server 添加到 Windows Server Core 版本上的实例时, 存在一个已知问题。 此问题已解决。 如果遇到此问题, 你可以应用[KB3164398](https://support.microsoft.com/kb/3164398)中所述的修补程序, 以将 R 功能添加到 Windows Server Core 上的现有实例中。 有关详细信息，请参阅 [不能在 Windows Server Core 操作系统上安装 Microsoft R Server 独立版](https://support.microsoft.com/kb/3168691)。


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>SQL Server 2016 的本地化版本的机器学习组件的脱机安装

早期版本的 SQL Server 2016 无法在没有 internet 连接的情况下在脱机安装过程中安装特定于区域设置的 .cab 文件。 此问题已在以后的版本中解决, 但是如果安装程序返回一条消息, 指出无法安装正确的语言, 则可以编辑该文件名, 以允许安装程序继续。

+ 手动编辑安装程序文件以确保安装了正确的语言。 例如, 若要安装日语版的 SQL Server, 请将文件的名称从 SRS_ 8.0.3.0 _**1033**更改为 srs_ 8.0.3.0 _**1041**。
+ 用于机器学习组件的语言标识符必须与 SQL Server 安装语言相同, 否则无法完成安装。

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>预发布版本: 支持策略、升级和已知问题

不再支持的任何预发行版本的[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]新安装。 如果使用的是预发行版本, 请尽快升级。

本部分包含有关特定升级方案的详细说明。

### <a name="how-to-upgrade-sql-server"></a>如何升级 SQL Server

您可以通过重新运行安装向导来升级您的 SQL Server 版本。

+ [升级 SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
+ [使用安装向导升级 SQL Server](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

您可以使用称为 "绑定" 的过程来仅升级机器学习组件: 
+ [使用 SqlBindR 升级机器学习组件](../install/upgrade-r-and-python.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>支持从预发行版本就地升级

不再支持从 SQL Server 2016 的预发行版本升级。 这包括 SQL Server 2016 CTP3、CTP 3.1、CTP 3.2、RC0 或 RC1。

以下版本随 SQL Server 2016 的预发行版本一起安装。

| Version | Build         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

如果对所使用的版本有任何疑问, 请在 SQL Server Management Studio `@@VERSION`中的查询中运行。

通常, 升级过程如下所示:

1. 备份脚本和数据。
2. 卸载预发布版本。
3. 安装发布版本。

卸载 SQL Server 机器学习组件的预发行版本可能比较复杂, 可能需要运行特殊的脚本。 请与技术支持联系以获取帮助。

###  <a name="bkmk_Uninstall"></a>从较旧版本的 Microsoft R Server 升级之前卸载

如果安装了 Microsoft R Server 的预发布版本，必须先卸载它，才能升级到较新版本。

1.  在“控制面板”  中，单击“添加或删除程序”  ，然后选择 `Microsoft SQL Server 2016 <version number>`。

2.  在具有“添加”  、“修复”  或“删除”  组件选项的对话框中，选择“删除”  。
  
3.  在“选择功能”  页面上的“共享功能”  下，选择“R Server（独立版）”  。 单击“下一步”  ，然后单击“完成”  ，卸载所选组件。

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>R Services 和 R Server (独立) 并行错误 

在早期版本的 SQL Server 2016 中, 同时安装 R Server (独立版) 和 R Services (数据库内) 有时会导致安装程序失败并出现 "拒绝访问" 消息。 此问题已在 Service Pack 1 中修复 SQL Server 2016。

如果遇到此错误, 并且需要升级这些功能, 请执行 SQL Server 2016 SP1 的滑出。 可以通过两种方法解决此问题, 这两种方法都需要卸载和重新安装。

1. 卸载 R Services (数据库内), 并确保已删除 SQLRUserGroup 的用户帐户。

2. 重新启动服务器, 然后重新安装 R Server (独立版)。

3. 再次运行 SQL Server 安装程序, 此时选择 "**向现有 SQL Server 中添加功能**"。

4. 选择该实例, 然后选择要添加的**R Services (数据库内)** 选项。

如果此过程未能解决此问题, 请尝试以下解决方法:

1. 同时卸载 R Services (数据库内) 和 R Server (独立版)。

2. 删除本地用户帐户 (SQLRUserGroup)。

3. 重新启动服务器。

4. 运行 SQL Server 安装程序, 并仅添加 "R Services (数据库内)" 功能。 不要选择**R Server (独立版)** 。

通常, 我们建议你不要在同一台计算机上安装 R Services (数据库内) 和 R Server (独立版)。 但是, 假设服务器有足够的容量, 你可能会发现 R Server 独立版可能会用作开发工具。 另一种可能的情况是需要使用 R Server 的操作化功能, 但也希望在不移动数据的情况下访问 SQL Server 数据。

## <a name="incompatible-version-of-r-client-and-r-server"></a>R Client 与 R Server 的版本不兼容

如果安装 Microsoft R Client 并将其用于在远程 SQL Server 计算上下文中运行 R, 可能会收到类似于下面的错误:

*你的计算机上运行的 Microsoft R 客户端版本为 9.0.0, 这与 Microsoft R Server 版本8.0.3 不兼容。请下载并安装兼容版本。*

在 SQL Server 2016 中, 需要在 SQL Server R Services 中运行的 R 版本与 Microsoft R Client 中的库完全相同。 此要求已在更高版本中删除。 但是, 我们建议你始终获取最新版本的机器学习组件, 并安装所有 service pack。 

如果你使用的是早期版本的 Microsoft R Server 并且需要确保与 Microsoft R Client 9.0.0 兼容, 请安装本[支持文章](https://support.microsoft.com/kb/3210262)中所述的更新。


## <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>安装失败，显示错误：“一次只能安装一个 Revolution Enterprise 产品”。

如果安装了较老的 Revolution Analytics 产品或 SQL Server R Services 的预发行版本，可能会遇到此错误。 安装较新版本的 Microsoft R Server 之前，必须先卸载任何以前的版本。 不支持与其他版本的 Revolution Enterprise 工具一起并行安装。

但是，如果将 R Server 独立版与 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 或 SQL Server 2016 配合使用，则支持并行安装。

## <a name="registry-cleanup-to-uninstall-older-components"></a>用于卸载较旧组件的注册表清理

如果删除较旧版本时遇到问题，可能需要编辑注册表以删除相关项。

> [!IMPORTANT]
> 此问题仅在安装了预发布版 Microsoft R Server 或 CTP 版 SQL Server 2016 R Services 时才出现。
  
1. 打开 Windows 注册表，并找到此项： `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`。
2. 如果存在以下条目且项仅包含值 `sEstimatedSize2`，请删除这些条目：
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972（针对 8.0.2）
  
    -   46695879-954E-4072-9D32-1CC84D4158F4（针对 8.0.1）
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B（针对 8.0.0）
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A（针对 7.5.0）

## <a name="see-also"></a>请参阅

 [SQL Server 机器学习服务 (数据库内)](../r/sql-server-r-services.md)

 [SQL Server Machine Learning Server (独立)](../r/r-server-standalone.md)
