---
title: "创建独立版 R Server | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 408e2503-5c7d-4ec4-9d3d-bba5a8c7661d
caps.latest.revision: 35
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4f39a03ecf7b74e0e1305d692a71c28609c80bf0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-standalone-r-server"></a>创建 R Server（独立版）

SQL Server 安装程序包括用于安装的机器学习在 SQL Server 外部运行的服务器的选项。 

此选项可能会很有用，如果你需要开发在 Windows 上，高性能 R 解决方案，然后在其他平台之间共享解决方案。 你还可以使用服务器选项设置的环境可用于构建解决方案，在这些执行支持远程计算上下文为：
  
  + 运行 R Services 的 SQL Server 实例
  + 使用 Hadoop 或 Spark 群集的 R Server 实例
  + Teradata 数据库内分析
  + 在 Linux 中运行的 R Server 

本主题介绍 Microsoft R Server 和 Microsoft 机器学习 Server 在 SQL Server 安装程序的安装步骤。

## <a name="which-should-i-install"></a>这应安装？

**Microsoft R Server**第一次提供的 SQL Server 2016 的一部分并支持 R 语言。 Microsoft R Server 的最后一个版本是 9.0.1。
已在 SQL Server 自 2017 年，重命名 R Server **Microsoft 机器学习 Server**，与添加 Python 的支持。 Microsoft 机器学习 Server 的最新版本是 9.1.0。

Microsoft R Server 和 Microsoft 机器学习服务器都需要 Enterprise Edition。

+ [安装 Microsoft R Server （独立） 使用 SQL Server 安装程序](#bkmk_installRServer)
+ [安装 Microsoft 机器学习 Server （独立） 使用 SQL Server 安装程序](#bkmk_installRServer) 

  安装时需要 SQL Server 许可证；可升级的时间通常与 SQL Server 的发行步调保持一致。 这可以确保你的开发工具与 SQL Server 计算上下文中运行的版本保持同步。

+ [安装 R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)

  使用此选项，R Server 安装使用现代的生命周期支持策略。 你还可以在安装程序以升级的 SQL Server 2016 实例后运行此安装程序。 目前，你_无法_安装 Python 支持使用此选项。 若要获取 Python，必须安装使用 SQL Server 2017 安装程序的机器学习服务器。

##  <a name="bkmk_installRServer"></a>如何安装 Microsoft 机器学习 Server （独立）
  
1. 如果已安装 Microsoft R Server 早期版本，我们建议你先卸载。

2. 运行 SQL Server 2017 安装程序。
  
3. 单击**安装**选项卡，然后选择**新计算机学习 Server （独立） 安装**。

4. 规则检查完成后，请接受 SQL Server 许可条款，然后选择新的安装。

5. 上**功能选择**页上，以下选项应已选择：
    
    - Microsoft 机器学习 Server （独立）
    
    - 默认值同时选中 R 和 Python。
    
    应忽略所有其他选项。

6.  接受许可条款下载和安装机器学习组件。 为 Microsoft R Open 和 Python 需要单独的许可协议。 
    
    当“接受”  按钮变为不可用时，可以单击“下一步” 。 
    
    安装这些组件（以及它们可能需要的任何必备项）可能需要花费一些时间。 
    
    如果计算机没有 Internet 访问权限，则应提前下载的组件安装程序。 有关详细信息，请参阅[没有 Internet 访问权限的安装 ML 组件](./installing-ml-components-without-internet-access.md)。 
    
7.  在“准备安装”  页上，验证选择，并单击“安装” 。


有关自动安装或脱机安装的详细信息，请参阅 [从命令行安装 Microsoft R Server](../../advanced-analytics/r-services/install-microsoft-r-server-from-the-command-line.md)。

###  <a name="bkmk_installRServer"></a> 安装 Microsoft R Server（独立版）  

1. 如果你已安装 Microsoft R Server 的以前版本或任何版本的 Revolution Analytics 工具，则必须先卸载它。  请参阅 [从 Microsoft R Server 的旧版本升级](#bkmk_Uninstall)。

2. 运行 SQL Server 2016 安装程序。 我们建议你安装 Service Pack 1 或更高版本。

3. 在“安装”  选项卡上，单击“新的 R Server（独立版）安装”  。
    
     ![R Server 独立版的安装选项](media/rsql-rstandalonesetup.png "R Server 独立版的安装选项")
    
4.  在“功能选择”  页上，应已选择以下选项：
    
    **R Server（独立版）**  
    
    应忽略所有其他选项。 不要将 SQL Server databae 引擎或 SQL Server R Services。
    
5.  接受下载和安装 Microsoft R Open 的许可条款。 当“接受”  按钮变为不可用时，可以单击“下一步” 。 
    
    安装这些组件（以及它们可能需要的任何必备项）可能需要花费一些时间。
    
6.  在“准备安装”  页上，验证选择，并单击“安装” 。  


### <a name="upgrade-an-existing-r-server-to-901"></a>将现有 R 服务器升级到 9.0.1

如果你安装 Microsoft R Server （独立版） 的早期版本可以升级要使用的 R 组件的较新版本的实例。 升级也会更改服务器现代生命周期支持策略。 这样，要不是 SQL Server 释放，更频繁地更新按不同的计划的实例。

1. 如果尚未安装，请安装 Microsoft R Server（独立版）。

2. 单独的基于 Windows 的安装位置从此处列出的下载：[运行 Microsoft R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#howtoinstall)。

3. 运行安装程序，并按照[这些说明](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#download-r-server-installer)。


### <a name="change-in-default-folder-for-r-packages"></a>更改默认文件夹 R 包

在安装使用 SQL Server 安装程序时，R 库安装在与用于安装的 SQL Server 版本关联的文件夹。 在此文件夹中，还可以找到示例数据、R 基础包的文档以及 R 工具和运行时的文档。

**使用 SQL Server 2016 安装 R Server（独立版）**

`C:\Program Files\Microsoft SQL Server\130\R_SERVER`

**使用 SQL Server 2017 安装 R Server（独立版）**

`C:\Program Files\Microsoft SQL Server\140\R_SERVER`

**使用 Windows 独立安装程序设置**

但是，如果使用单独的 Windows 安装程序中，安装或升级使用单独的 Windows installer，R 库转移到以下 R Server 文件夹：

`C:\Program Files\Microsoft\R Server\R_SERVER`
      
**R 服务或机器学习的安装程序服务数据库中**

如果你安装的 SQL Server 实例 R Services （数据库） 或机器学习服务 （数据库中），并且该实例是同一台计算机上，R 库和工具默认安装到另一个文件夹：

`C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES`

不要直接调用与 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例关联的 R 包或实用工具。 如果 R Server 和 R Services 安装在同一计算机上需要进行 RGui 或其他工具运行时，，使用的 R 工具和 R_SERVER 文件夹所安装的包。


### <a name="development-tools"></a>开发工具

开发 IDE 不会安装安装程序的一部分。 不需要其他工具，如所有标准工具，将包括，将向你提供的 R 或 Python 的分布。

我们建议你尝试的新发行版[!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]，如 Visual Studio 支持 R 和 Python 以及 SQL Server 和 BI 工具。 但是，你可以使用任何首选的开发环境，包括 RStudio。

## <a name="troubleshooting"></a>故障排除  

### <a name="incompatible-version-of-r-client-and-r-server"></a>R Client 与 R Server 的版本不兼容

如果安装最新版本的 Microsoft R Client，并使用它在远程计算机环境中的 SQL Server 上运行 R，则可能收到以下错误：

*计算机上运行的 Microsoft R Client 版本为 9.0.0，与 8.0.3 版的 Microsoft R Server 不兼容。请下载并安装兼容版本。

通常情况下，随 SQL Server R Services 一起安装的 R 版本会在发布 Service Release 后进行更新。 若要确保始终拥有最新版本的 R 组件，请安装所有 Service Pack。 为了与 Microsoft R Client 9.0.0 兼容，必须安装本 [支持文章](https://support.microsoft.com/kb/3210262)中介绍的更新。 


### <a name="installing-microsoft-r-server-on-an-instance-of-sql-server-installed-on-windows-core"></a>在 Windows Core 上安装的 SQL Server 实例上安装 Microsoft R Server

在 SQL Server 2016 RTM 版本中，没有已知的问题时 Microsoft R Server 添加到 Windows Server Core 版本上的实例。 此问题已解决。

如果遇到此问题，可以应用 [KB3164398](https://support.microsoft.com/kb/3164398) 中介绍的解决方法向 Windows Server Core 上的现有实例添加 R 功能。   有关详细信息，请参阅 [不能在 Windows Server Core 操作系统上安装 Microsoft R Server 独立版](https://support.microsoft.com/kb/3168691)。


###  <a name="bkmk_Uninstall"></a> 从 Microsoft R Server 的旧版本升级

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

[Microsoft R Server](../../advanced-analytics/r-services/r-server-standalone.md)


