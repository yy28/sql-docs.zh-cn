---
title: "机器学习服务器独立服务器或 R Server 独立安装 |Microsoft 文档"
ms.custom: 
ms.date: 02/14/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 408e2503-5c7d-4ec4-9d3d-bba5a8c7661d
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 2ecb60bd02b3fc1ee7ac7101749fa7affc2523bd
ms.sourcegitcommit: 6bd21109abedf64445bdb3478eea5aaa7553fa46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2018
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone"></a>安装机器学习 Server （独立） 或 R Server （独立）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 安装程序包括用于安装的机器学习在 SQL Server 外部运行的服务器的选项。 此选项可能会很有用，如果你需要开发高性能计算机学习解决方案，可以使用远程计算上下文，或者，可以部署到多个平台，包括：
  
  + SQL Server 2016 或 SQL Server 自 2017 年 1 中启用机器学习的实例
  + Hadoop 或 Spark 群集中的 R 服务器或计算机学习服务器实例
  + R Server 或 Linux 中的机器学习服务器

本文介绍如何使用 SQL Server 安装程序安装的计算机学习服务器或 Microsoft R Server 的独立版本。 如果你有企业版或软件保障，安装独立机器学习服务器是免费的。

+ [安装 R Server](#bkmk_installRServer) -使用 SQL Server 2016 安装程序
+ [安装 Server 机学习](#bkmk_installMLServer)-使用 SQL Server 2017 安装程序
+ [Microsoft R Server 的现有实例升级](#bkmk_upgrade)
+ [帮助我确定要安装的内容](#bkmk_tips)

##  <a name="bkmk_installMLServer"></a> 安装机器学习 Server （独立）

此功能需要企业许可证或等效**SQL Server 2017**。

如果已安装 Microsoft R Server 早期版本，我们建议你先卸载。

如果计算机没有 Internet 访问权限，则应提前下载的组件安装程序。 有关详细信息，请参阅[安装没有 internet 访问权限的机器学习组件](./installing-ml-components-without-internet-access.md)。

1. 运行 SQL Server 2017 安装程序。

2. 单击**安装**选项卡，然后选择**新计算机学习 Server （独立） 安装**。
    
     ![安装机器学习服务器独立](media/2017setup-installation-page-mlsvr.png "启动机器学习 Server 独立安装")

3. 规则检查完成后，请接受 SQL Server 许可条款，然后选择新的安装。

4. 上**功能选择**页上，以下选项应已处于选中状态：

    - Microsoft 机器学习 Server （独立）

    - 默认值同时选中 R 和 Python。 您可以取消选中其中任一种语言，但我们建议你安装至少一个受支持的语言。

     ![安装机器学习服务器独立](media/2017setup-features-page-mlsvr-rpy.png "启动机器学习 Server 独立安装")
    
    应忽略所有其他选项。 
    
    > [!NOTE]
    > 请避免先安装**共享功能**如果计算机已安装的 SQL Server 数据库中分析的机器学习服务。 这将创建重复的库。
    > 
    > 此外，在 SQL Server 中运行的 R 或 Python 脚本由 SQL Server，以免与其他数据库引擎服务使用的内存发生冲突，而独立机器学习服务器没有此类约束，并且可能会干扰其他数据库操作. 最后，数据库管理员通常阻止通过 RDP 会话中，它通常用于操作化，远程访问。
    > 
    > 出于这些原因，我们通常建议你从 SQL Server 机器学习服务的单独计算机上安装机器学习 Server （独立）。

5.  接受许可条款下载和安装机器学习组件。 如果你安装这两种语言，单独的许可协议则需要为 Microsoft R 和 Python。
    
     ![Python 许可协议](media/2017setup-python-license.png "Python 许可协议")
    
    这些组件，以及它们可能需要的任何系统必备组件的安装过程可能需要一段时间。 当“接受”  按钮变为不可用时，可以单击“下一步” 。

6.  在“准备安装”  页上，验证选择，并单击“安装” 。

有关自动安装或脱机安装的详细信息，请参阅[从命令行中安装 Microsoft R Server](../../advanced-analytics/r/install-microsoft-r-server-from-the-command-line.md)。

##  <a name="bkmk_installRServer"></a> 安装 Microsoft R Server（独立版）

此功能需要企业许可证或等效**SQL Server 2016**。

如果已安装任何以前版本的 Revolution Analytics 工具或包，你必须先卸载它们。 请参阅[从较旧版本的 Microsoft R Server 升级](#bkmk_Uninstall)。

1. 运行 SQL Server 2016 安装程序。 我们建议你安装 Service Pack 1 或更高版本。

2. 上**安装**选项卡上，单击**新 R Server （独立） 安装**。
    
     ![启动的 R Server 独立安装程序](media/2016-setup-installation-rsvr.png "启动的 R Server 独立安装程序")
    
3.  在“功能选择”  页上，应已选择以下选项：
    
    **R Server（独立版）**  
    
    ![功能选择 R Server 独立](media/2016setup-rserver-features.png "功能 R Server 独立的选择")
    
    应忽略所有其他选项。 
    
    > [!NOTE]
    > 请避免先安装**共享功能**如果你运行安装程序的计算机上其中 R Services 已安装的 SQL Server 数据库中分析。 这将创建重复的库。
    > 
    > 由 SQL Server，以免与其他数据库引擎服务使用的内存发生冲突，在 SQL Server 中运行的 R 脚本进行管理，而独立 R Server 没有此类约束，并可能会干扰其他数据库操作。
    > 
    > 我们通常建议你从 SQL Server 机器学习服务的单独计算机上安装机器学习 Server （独立）。

4.  接受下载和安装 Microsoft R Open 的许可条款。 当“接受”  按钮变为不可用时，可以单击“下一步” 。
    
    这些组件，以及它们可能需要的任何系统必备组件的安装过程可能需要一段时间。
    
5.  在“准备安装”  页上，验证选择，并单击“安装” 。

## <a name="bkmk_upgrade"></a> R Server 的现有实例升级

如果你安装 Microsoft R Server （独立版） 的早期版本，你可以升级要使用的 R 组件的较新版本的实例。 升级也会更改要使用现代软件生命周期支持策略的支持策略。 这样，要不是 SQL Server 释放，更频繁地更新按不同的计划的实例。

1. 从此处列出的位置下载单独的基于 Windows 的安装： 

    + [安装机器学习适用于 Windows 的服务器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
    + [适用于 Windows 安装 R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)

2. 运行安装程序，然后按照说明。 在其中选择要安装的功能页上，选择你想要升级的 R Server 的每个实例。

## <a name ="bkmk_tips"></a> 安装提示和后续步骤

本部分提供与设置相关的其他信息。

### <a name="which-version-should-i-install"></a>应安装哪个版本？

+ **Microsoft R Server**第一次提供的 SQL Server 2016 的一部分并支持 R 语言。 Microsoft R Server 的最后一个版本是 9.0.1。

+ **Microsoft 机器学习 Server**最新版本，也不能随 SQL Server 自 2017 年发布功能许多更新，包括支持 Python。 已发布 SQL Server 自 2017 年的累积更新 1，其中包括 9.2.1.24 新版机器学习服务器。 如果你想最新的 Python Api，我们建议此更新。

+ **就地升级**： 安装程序要求 SQL Server 许可证和升级通常与 SQL Server 发布节奏对齐。 这可以确保你的开发工具与 SQL Server 计算上下文中运行的版本保持同步。 但是，你可以使用单独的基于 Windows 的安装程序来获取更频繁更新，现代软件生命周期支持策略下。 此安装程序还可用于升级的 SQL Server 2016 或 SQL Server 2017 实例。

### <a name="default-installation-folders"></a>默认安装文件夹

安装 R Server 时或使用 SQL Server 安装程序的机器学习服务器，R 库安装在与用于安装的 SQL Server 版本关联的文件夹。 在此文件夹中，你会发现示例数据、 R 基程序包，文档和文档的 R 工具和运行时。

但是，如果使用单独的 Windows 安装程序中，安装或升级使用单独的 Windows installer，R 库安装在不同的文件夹。

只是为了引用，如果你已安装的 SQL Server 实例与 R Services （数据库） 或机器学习服务 （数据库中），并且该实例是在同一台计算机，R 库和工具默认安装在其他文件夹中。

下表列出每个安装的路径。

|版本| 安装方法 | 默认文件夹|
|----|----|----|
|R Server (Standalone) |SQL Server 2016 安装程序向导|`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|R Server (Standalone) |Windows 独立安装程序|`C:\Program Files\Microsoft\R Server\R_SERVER`|
|机器学习服务器（独立） |  自 2017 年 SQL Server 安装向导中，与 R 语言选项 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER`|
|机器学习服务器（独立） |  自 2017 年 SQL Server 安装向导中，与 Python 语言选项 |`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|机器学习服务器（独立） |  Windows 独立安装程序 |`C:\Program Files\Microsoft\R Server\R_SERVER`|
|R Services（数据库内） |SQL Server 2016 安装程序向导|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|
|机器学习服务（数据库内） |自 2017 年 SQL Server 安装向导中，与 R 语言选项|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  |
|机器学习服务（数据库内） |自 2017 年 SQL Server 安装向导中，与 Python 语言选项| `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
### <a name="development-tools"></a>开发工具

开发 IDE 不会安装安装程序的一部分。 不需要其他工具，如所有标准工具，将包括，将向你提供的 R 或 Python 的分布。

我们建议你尝试的新发行版[!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]。 Visual Studio 支持同时 R 和 Python，以及数据库开发工具，与 SQL Server 的连接和 BI 工具。 但是，你可以使用任何首选的开发环境，包括 RStudio。

## <a name="troubleshooting"></a>故障排除

本部分列出了一些常见的问题时应注意的安装的计算机学习服务器或 R Server。

### <a name="incompatible-version-of-r-client-and-r-server"></a>R Client 与 R Server 的版本不兼容

如果你安装 Microsoft R 客户端，并使用它的远程 SQL Server 计算上下文中运行 R，可能会出现如下错误：

*运行的你在计算机上，这与 Microsoft R Server 版本 8.0.3 不兼容的版本 9.0.0 的 Microsoft R 客户端。请下载并安装兼容版本。

在 SQL Server 2016 中，它是必需的 SQL Server R Services 中所运行的 R 版本正好为在 Microsoft R 客户端库相同。 更高版本中已删除该需求。 但是，我们建议你始终获取最新版本的机器学习组件，并安装所有 service pack。 

如果你有 Microsoft R Server 的早期版本，且需要确保与 Microsoft R 客户端 9.0.0 兼容性，在此安装所述的更新[支持文章](https://support.microsoft.com/kb/3210262)。

### <a name="installing-microsoft-r-server-on-an-instance-of-sql-server-installed-on-windows-core"></a>在 Windows Core 上安装的 SQL Server 实例上安装 Microsoft R Server

在 SQL Server 2016 RTM 版本中，没有已知的问题时 Microsoft R Server 添加到 Windows Server Core 版本上的实例。 此问题已解决。

如果你遇到此问题，则可以应用中所述的修复[KB3164398](https://support.microsoft.com/kb/3164398)将 R 功能添加到 Windows Server Core 上的现有实例。   有关详细信息，请参阅 [不能在 Windows Server Core 操作系统上安装 Microsoft R Server 独立版](https://support.microsoft.com/kb/3168691)。

###  <a name="bkmk_Uninstall"></a> 从 Microsoft R Server 的较旧版本升级

如果安装了 Microsoft R Server 的预发布版本，必须先卸载它，才能升级到较新版本。

**卸载 R Server（独立版）**

1.  在“控制面板” 中，单击“添加或删除程序” ，然后选择 `Microsoft SQL Server 2016 <version number>`。

2.  在具有“添加” 、“修复” 或“删除”  组件选项的对话框中，选择“删除” 。
  
3.  在“选择功能”  页面上的“共享功能” 下，选择“R Server（独立版）” 。 单击“下一步” ，然后单击“完成”  ，卸载所选组件。

### <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>安装失败，显示错误：“一次只能安装一个 Revolution Enterprise 产品”。

如果安装了较老的 Revolution Analytics 产品或 SQL Server R Services 的预发行版本，可能会遇到此错误。 安装较新版本的 Microsoft R Server 之前，必须先卸载任何以前的版本。 不支持与其他版本的 Revolution Enterprise 工具一起并行安装。

但是，如果将 R Server 独立版与 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 或 SQL Server 2016 配合使用，则支持并行安装。

### <a name="unable-to-uninstall-older-components"></a>无法卸载较旧的组件

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

[机器学习服务器（独立）](../../advanced-analytics/r/r-server-standalone.md)
