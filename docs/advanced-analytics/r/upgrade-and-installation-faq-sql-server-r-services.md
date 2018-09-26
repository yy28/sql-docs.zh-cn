---
title: SQL Server 机器学习的升级和安装常见问题解答 |Microsoft Docs
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/15/2018
ms.topic: conceptual
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.openlocfilehash: 37cd28b895c66d6ddcf1517e79ef6bf4537e2a96
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "46712299"
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>SQL Server 机器学习或 R Server 的升级和安装常见问题解答
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本主题提供有关安装机器学习中 SQL Server 功能的一些常见问题的解答。 它还介绍了有关升级的常见问题。

+ 某些问题只是出现升级预发行版中。 因此，我们建议您确定你的版本和版本首次在阅读这些说明之前。 若要获取版本信息，请运行`@@VERSION`在从 SQL Server Management Studio 查询中。
+ 升级到最新版本或 service 版本尽可能快地解决最新版本中已修复任何问题。

**适用于：** SQL Server 2016 R Services、 SQL Server 2017 机器学习服务 （数据库内）

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>要求和限制的较旧版本的 SQL Server 2016 

具体取决于要安装的 SQL Server 的版本，以下限制的一些可能适用：

- 在早期版本的 SQL Server 2016 R Services，包含的工作目录的驱动器上需要 8dot3 表示法。 如果安装的预发行版本，则升级到 SQL Server 2016 Service Pack 1 应修复此问题。 此要求不适用于版本后 SP1。

- 目前，无法安装[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]故障转移群集上。 不过，SQL Server 2019 预览确实提供故障转移支持，如果想要评估测试环境中的此 capablity。 有关详细信息，请参阅[What's New](../what-s-new-in-sql-server-machine-learning-services.md)。

- Azure VM 上可能需要一些额外的配置。 例如，您可能需要创建防火墙例外，以支持远程访问。

- 不支持通过并行安装的 R，另一个版本或 Revolution Analytics 中的其他版本。

- 禁用病毒扫描开始安装程序之前。 安装程序完成后，我们建议挂起病毒扫描使用的文件夹上[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]。 最好是挂起整个扫描[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]树。

 - 在 Windows Core 上安装的 SQL Server 实例上安装 Microsoft R Server。 在 RTM 版本的 SQL Server 2016 中，没有已知的问题时将 Microsoft R Server 添加到 Windows Server Core 版本上的实例。 此问题已解决。 如果遇到此问题，可以在应用中所述的修补[KB3164398](https://support.microsoft.com/kb/3164398)将 R 功能添加到 Windows Server Core 上的现有实例。 有关详细信息，请参阅 [不能在 Windows Server Core 操作系统上安装 Microsoft R Server 独立版](https://support.microsoft.com/kb/3168691)。


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>有关 SQL Server 2016 的本地化版本的机器学习组件的脱机安装

SQL Server 2016 的早期发行版本无法在没有 internet 连接的脱机安装过程中安装特定于区域设置的.cab 文件。 更高版本中已修复此问题，但如果安装程序将返回一条消息指出它不能安装正确的语言，则可以编辑的文件名，以允许安装程序继续。

+ 手动编辑该安装程序文件，以确保安装正确的语言。 例如，若要安装日语版 SQL Server，你将更改的文件的名称从 SRS_8.0.3.0_**1033年**.cab 为 SRS_8.0.3.0_**1041年**.cab。
+ 机器学习组件使用的语言标识符必须是 SQL Server 安装程序语言，与相同或无法完成安装程序。

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>预发布版本： 支持策略、 升级和已知的问题

新安装的任何预发行版本的[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]不再受支持。 如果使用的预发行版本，则升级越早越好。

本部分包含有关特定的升级方案的详细的说明。

### <a name="how-to-upgrade-sql-server"></a>如何升级 SQL Server

你可以通过重新运行安装向导升级你的 SQL Server 版本。

+ [升级 SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
+ [使用安装向导升级 SQL Server](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

你可以升级只是机器学习组件使用名为绑定的过程： 
+ [使用 SqlBindR 升级机器学习组件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>结束对从预发行版本的就地升级支持

不再支持从 SQL Server 2016 的预发布版本升级。 这包括 SQL Server 2016 CTP3、 CTP3.1、 CTP3.2、 RC0 或 RC1。

以下版本随 SQL Server 2016 的预发布版本一起安装。

| 版本 | 生成         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

如果你不的确定使用哪一版本，运行`@@VERSION`在从 SQL Server Management Studio 查询中。

一般情况下，升级的过程如下所示：

1. 备份脚本和数据。
2. 卸载预发行版本。
3. 安装发行版本。

正在卸载预发行版本的 SQL Server 机器学习组件可能复杂，可能需要运行特殊的脚本。 请与技术支持联系以获取帮助。

###  <a name="bkmk_Uninstall"></a> 卸载然后再从较旧版本的 Microsoft R Server 升级

如果安装了 Microsoft R Server 的预发布版本，必须先卸载它，才能升级到较新版本。

1.  在“控制面板” 中，单击“添加或删除程序” ，然后选择 `Microsoft SQL Server 2016 <version number>`。

2.  在具有“添加” 、“修复” 或“删除”  组件选项的对话框中，选择“删除” 。
  
3.  在“选择功能”  页面上的“共享功能” 下，选择“R Server（独立版）” 。 单击“下一步” ，然后单击“完成”  ，卸载所选组件。

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>R Services 和 R Server （独立版）-同时错误 

在早期版本的 SQL Server 2016 中，安装 R Server （独立版） 和 R Services （数据库内） 在同一时间有时会导致安装程序失败并显示"拒绝访问"消息。 为 SQL Server 2016 Service Pack 1 中修复此问题。

如果您遇到此错误，并且需要升级这些功能，执行 SQL Server 2016 sp1 的 slipstream 安装。 有两种方法来解决此问题，这两者需要卸载并重新安装。

1. 卸载 R Services （数据库内），并确保删除 SQLRUserGroup 的用户帐户。

2. 重新启动服务器，并重新安装 R Server （独立版）。

3. 运行的 SQL Server 安装程序一次的详细信息，并选择这一次**添加到现有的 SQL Server 的功能**。

4. 选择该实例，然后选择**R Services （数据库内）** 添加选项。

如果此过程无法解决该问题，请尝试以下解决方法：

1. 在同一时间卸载 R Services （数据库内） 和 R Server （独立版）。

2. 删除本地用户帐户 (SQLRUserGroup)。

3. 重新启动服务器。

4. 运行 SQL Server 安装程序，并添加 R Services （数据库内） 功能仅。 不要选择**R Server （独立版）**。

通常情况下，我们建议你不要安装 R Services （数据库内） 和 R Server （独立版） 在同一台计算机上。 但是，如果服务器具有足够的容量，你可能会发现 R Server 独立版可作为开发工具。 另一种情形是，您需要使用的 R Server 操作化功能，但同时想要访问 SQL Server 数据，而不移动数据。

## <a name="incompatible-version-of-r-client-and-r-server"></a>R Client 与 R Server 的版本不兼容

如果你安装 Microsoft R 客户端，并使用它的远程 SQL Server 计算上下文中运行 R，可能会收到如下错误：

*您您与 Microsoft R Server 8.0.3 版不兼容的计算机上运行 Microsoft R client 9.0.0 的版。请下载并安装兼容版本。

在 SQL Server 2016 中，它是必需的 SQL Server R Services 中运行的 R 版本完全是与 Microsoft R Client 中的库相同。 更高版本中已经删除了这一要求。 但是，我们建议您始终获取最新版本的机器学习组件，并安装所有 service pack。 

如果您具有早期版本的 Microsoft R Server，并且需要以确保与 Microsoft R Client 9.0.0 兼容，在此安装所述的更新[支持文章](https://support.microsoft.com/kb/3210262)。


## <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>安装失败，显示错误：“一次只能安装一个 Revolution Enterprise 产品”。

如果安装了较老的 Revolution Analytics 产品或 SQL Server R Services 的预发行版本，可能会遇到此错误。 安装较新版本的 Microsoft R Server 之前，必须先卸载任何以前的版本。 不支持与其他版本的 Revolution Enterprise 工具一起并行安装。

但是，如果将 R Server 独立版与 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 或 SQL Server 2016 配合使用，则支持并行安装。

## <a name="registry-cleanup-to-uninstall-older-components"></a>若要卸载较旧的组件的注册表清理

如果删除较旧版本时遇到问题，可能需要编辑注册表以删除相关项。

> [!IMPORTANT]
> 此问题仅在安装了预发布版 Microsoft R Server 或 CTP 版 SQL Server 2016 R Services 时才出现。
  
1. 打开 Windows 注册表，并找到此项： `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`。
2. 如果存在以下条目且项仅包含值 `sEstimatedSize2`，请删除这些条目：
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972（针对 8.0.2）
  
    -   46695879-954E-4072-9D32-1CC84D4158F4（针对 8.0.1）
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B（针对 8.0.0）
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A（针对 7.5.0）

## <a name="see-also"></a>另请参阅

 [SQL Server 机器学习服务 （数据库内）](../r/sql-server-r-services.md)

 [SQL Server 机器学习服务器 （独立版）](../r/r-server-standalone.md)
