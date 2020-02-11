---
title: 升级和安装常见问题解答
description: 解答在 SQL Server 中安装机器学习功能的一些常见问题。
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
ms.author: davidph
author: dphansen
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6357f98627842ab790b494cf1b4a1f9b2110ec9c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727346"
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>SQL Server 机器学习或 R Server 的升级和安装常见问题解答
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

该主题提供了在 SQL Server 中安装机器学习功能的一些常见问题的解答。 还涉及有关升级的常见问题。

+ 仅从预发行版本进行升级会出现某些问题。 因此，建议在阅读这些说明之前先确定你的版本。 若要获取版本信息，请从 SQL Server Management Studio 的查询中运行 `@@VERSION`。
+ 请尽快升级到最新版本或服务版本，以解决最新版本中已解决的所有问题。

**适用于：** SQL Server 2016 R Services、SQL Server 机器学习服务（数据库内）

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>对旧版 SQL Server 2016 的要求和限制 

根据要安装的 SQL Server 的内部版本，可能会出现以下限制：

- 在早期版本的 SQL Server 2016 R Services 中，包含工作目录的驱动器上需要 8dot3 表示法。 如果安装了预发行版本，则升级到 SQL Server 2016 Service Pack 1 应该可以解决此问题。 此要求不适用于 SP1 之后的版本。

- 不能在 SQL Server 2016 中的故障转移群集上安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 但 SQL Server 2019 提供故障转移支持。 有关详细信息，请参阅[新增功能](../what-s-new-in-sql-server-machine-learning-services.md)。

- 在 Azure VM 上，可能需要进行其他配置。 例如，你可能需要创建防火墙例外以支持远程访问。

- 不支持另一 R 版本或 Revolution Analytics 中的其他版本来创建并行安装。

- 开始安装之前，请禁用病毒扫描。 安装完成后，建议在 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 使用的文件夹上挂起病毒扫描。 最好在整个 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 树上挂起扫描。

 - 在 Windows Core 上安装的 SQL Server 实例上安装 Microsoft R Server。 在 SQL Server 2016 的 RTM 版本中，将 Microsoft R Server 添加到 Windows Server Core 版本上的实例时有一个已知问题。 此问题已解决。 如果遇到此问题，可以应用 [KB3164398](https://support.microsoft.com/kb/3164398) 中介绍的解决方法向 Windows Server Core 上的现有实例添加 R 功能。 有关详细信息，请参阅 [不能在 Windows Server Core 操作系统上安装 Microsoft R Server 独立版](https://support.microsoft.com/kb/3168691)。


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>SQL Server 2016 本地化版本的机器学习组件的脱机安装

SQL Server 2016 的早期版本无法在没有 Internet 连接的脱机安装过程中安装特定于语言环境的 .cab 文件。 此问题在更高版本中已得到解决，但是如果安装程序返回一条消息，指出它无法安装正确的语言，则可以编辑文件名以允许安装继续。

+ 手动编辑安装程序文件以确保安装正确的语言。 例如，若要安装日语版 SQL Server，应将文件名称从 SRS_8.0.3.0_1033.cab 更改为 SRS_8.0.3.0_1041.cab   。
+ 机器学习组件使用的语言标识符必须与 SQL Server 安装程序语言相同，否则无法完成安装。

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>预发行版本：支持策略、升级和已知问题

不再支持重新安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的任何预发行版本。 如果使用的是预发行版本，请尽快升级。

本部分包含有关特定升级方案的详细说明。

### <a name="how-to-upgrade-sql-server"></a>如何升级 SQL Server

可以通过重新运行安装向导来升级 SQL Server 版本。

+ [升级 SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
+ [使用安装向导升级 SQL Server](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

可以使用称为“绑定”的过程来仅升级机器学习组件： 
+ [使用 SqlBindR 升级机器学习组件](../install/upgrade-r-and-python.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>对预发行版本的就地升级的支持终止

不再支持从 SQL Server 2016 的预发行版本进行升级。 这包括 SQL Server 2016 CTP3、CTP3.1、CTP3.2、RC0 或 RC1。

以下版本与 SQL Server 2016 的预发布版本一起安装。

| 版本 | 构建         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

如果对所使用的版本有任何疑问，请从 SQL Server Management Studio 的查询中运行 `@@VERSION`。

通常，升级过程如下所示：

1. 备份脚本和数据。
2. 卸载预发行版本。
3. 安装发行版本。

卸载 SQL Server 机器学习组件的预发布版本可能很复杂，并且可能需要运行某种特殊脚本。 请与技术支持联系以获取帮助。

###  <a name="bkmk_Uninstall"></a> 从 Microsoft R Server 的旧版本升级前先进行卸载

如果安装了 Microsoft R Server 的预发布版本，必须先卸载它，才能升级到较新版本。

1.  在“控制面板”  中，单击“添加或删除程序”  ，然后选择 `Microsoft SQL Server 2016 <version number>`。

2.  在具有“添加”  、“修复”  或“删除”  组件选项的对话框中，选择“删除”  。
  
3.  在“选择功能”  页面上的“共享功能”  下，选择“R Server（独立版）”  。 单击“下一步”  ，然后单击“完成”  ，卸载所选组件。

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>R Services 和 R Server（独立版）并行错误 

在 SQL Server 2016 的早期版本中，同时安装 R Server（独立版）和 R Services（数据库内）有时会导致安装失败，并显示“拒绝访问”消息。 SQL Server 2016 Service Pack 1 中已修复此问题。

如果遇到此错误，并且需要升级这些功能，请执行 SQL Server 2016 SP1 的补充安装。 有两种方法可以解决此问题，这两种方法都需要卸载并重新安装。

1. 卸载 R Services（数据库内），并确保已删除 SQLRUserGroup 的用户帐户。

2. 重启服务器，然后重新安装 R Server（独立版）。

3. 再次运行 SQL Server 安装程序，此时选择“将功能添加到现有 SQL Server 中”  。

4. 选择该实例，然后选择“R Services (数据库内)”选项进行添加  。

如果此过程无法解决问题，请尝试以下解决方法：

1. 同时卸载 R Services（数据内）和 R Server（独立版）。

2. 删除本地用户帐户 (SQLRUserGroup)。

3. 重新启动服务器。

4. 运行 SQL Server 安装程序，并仅添加 R Services（数据库内）功能。 不要选择“R Server（独立版）”  。

通常，建议不要在同一台计算机上同时安装 R Services（数据库内）和 R Server（独立版）。 但是，假设服务器容量足够大，你或许会发现 R Server 独立版是一个很有用的开发工具。 一种可能的情况是，需要使用 R Server 的操作功能，而且还希望在不移动数据的情况下访问 SQL Server 数据。

## <a name="incompatible-version-of-r-client-and-r-server"></a>R Client 与 R Server 的版本不兼容

如果安装 Microsoft R Client，并使用它在远程 SQL Server 计算上下文中运行 R，则可能收到类似以下的错误：

计算机上运行的 Microsoft R Client 版本为 9.0.0，与 8.0.3 版的 Microsoft R Server 不兼容 *。请下载并安装兼容版本。

在 SQL Server 2016 中，要求 SQL Server R Services 中运行的 R 版本与 Microsoft R Client 中的库完全相同。 以后的版本将消除此要求。 但是，建议始终获取机器学习组件的最新版本，并安装所有服务包。 

如果拥有 Microsoft R Server 的早期版本并需要确保与 Microsoft R Client 9.0.0 兼容，请安装本[支持文章](https://support.microsoft.com/kb/3210262)中介绍的更新。


## <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>安装失败，显示错误：“一次只能安装一个 Revolution Enterprise 产品”。

如果安装了较老的 Revolution Analytics 产品或 SQL Server R Services 的预发行版本，可能会遇到此错误。 安装较新版本的 Microsoft R Server 之前，必须先卸载任何以前的版本。 不支持与其他版本的 Revolution Enterprise 工具一起并行安装。

但是，如果将 R Server 独立版与 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 或 SQL Server 2016 配合使用，则支持并行安装。

## <a name="registry-cleanup-to-uninstall-older-components"></a>用于卸载旧组件的注册表清理

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

 [SQL Server 机器学习服务（数据库内）](../r/sql-server-r-services.md)

 [SQL Server Machine Learning Server（独立版）](../r/r-server-standalone.md)
