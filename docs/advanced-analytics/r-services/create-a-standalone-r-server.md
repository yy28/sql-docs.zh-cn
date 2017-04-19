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
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2fac63cc50814124aa47bd9eaed2e2fedacf7432
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-standalone-r-server"></a>创建 R Server（独立版）
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序包含用于安装 **Microsoft R Server（独立版）**的选项。 
  
  通常，如果你需要在 Windows 上开发高性能 R 解决方案，可能会安装 Microsoft R Server（独立版）。 可以在安装 R Server（独立版）的计算机本地运行解决方案，从而利用 ScaleR 技术来缩放和并行化 R 代码；或者，可以将解决方案部署到这些强大的计算上下文中：
  
  + 运行 R Services 的 SQL Server 实例
  + 使用 Hadoop 或 Spark 群集的 R Server 实例
  + Teradata 数据库内分析
  + 在 Linux 中运行的 R Server 
 
 有关详细信息，请参阅 [R Server 平台](https://www.microsoft.com/cloud-platform/r-server)和[包含的内容](#bkmk_Included)。
  
 Microsoft R Server 仅在 Enterprise Edition 中可用。  
  

## <a name="licensing-and-updates"></a>许可和更新
  
可以使用两种方法安装 Microsoft R Server：

+ 根据[此部分](#bkmk_installRServer)中所述，使用 SQL Server 安装向导创建适用于 Windows 的 R Server 独立安装。 

    安装时需要 SQL Server 许可证；可升级的时间通常与 SQL Server 的发行步调保持一致。 这可以确保你的开发工具与 SQL Server 计算上下文中运行的版本保持同步。

+ 根据[运行 Microsoft R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows) 中所述，单独使用全新简化的 Windows 安装程序。 

    运行此安装向导可在[新式生命周期](https://support.microsoft.com/help/447912)策略中注册实例。 此支持产品确保你始终使用最新的 R 版本。

> [!TIP]
> 还可以使用适用于 Microsoft R Server 的新 Windows 安装程序将 SQL Server 2016 R Services 的任何实例转换为新的支持策略。 如果你想要更频繁地更新 R 组件，此选项可能很合适。 有关详细信息，请参阅 [使用 sqlBindR.exe 升级 R Services 的实例](http://www.bing.com)的选项。   
  
##  <a name="bkmk_installRServer"></a>如何安装 Microsoft R Server（独立版）  
  
1.  如果已安装早期版本的 Microsoft R Server，必须先卸载它。  请参阅 [从 Microsoft R Server 的旧版本升级](#bkmk_Uninstall)。 

2. 运行 SQL Server 安装程序。  
  
2.  在“安装”  选项卡上，单击“新的 R Server（独立版）安装”  。  
  
     ![R Server 独立版的安装选项](../../advanced-analytics/r-services/media/rsql-rstandalonesetup.png "R Server 独立版的安装选项")  
  
3.  在“功能选择”  页上，应已选择以下选项：  
  
    -   **R Server（独立版）**  
  
         此选项将安装共享功能，包括开放源代码 R 工具和基础包，以及 Microsoft R 提供的增强 R 包和连接工具。  
  
     应忽略所有其他选项。  
  
4.  接受下载和安装 Microsoft R Open 的许可条款。 当“接受”  按钮变为不可用时，可以单击“下一步” 。 安装这些组件（以及它们可能需要的任何必备项）可能需要花费一些时间。   
  
5.  在“准备安装”  页上，验证选择，并单击“安装” 。  
  
> [!TIP]
> 有关自动安装或脱机安装的详细信息，请参阅 [从命令行安装 Microsoft R Server](../../advanced-analytics/r-services/install-microsoft-r-server-from-the-command-line.md)。

## <a name="how-to-upgrade-r-server-to-901"></a>如何将 R Server 升级到 9.0.1

如果已安装 Microsoft R Server（独立版），可将该实例升级为使用新的新式生命周期支持策略。 这样，便可以单独根据 SQL Server 支持计划，更频繁地更新实例。 

1. 如果尚未安装，请安装 Microsoft R Server（独立版）。

2. 下载适用于 R Server 9.0.1 的基于 Windows 的独立安装程序。 有关下载位置，请参阅[运行 Microsoft R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#howtoinstall)。

3. 运行安装程序并遵照[这些说明](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#download-r-server-installer)操作

  
 ## <a name ="bkmk_Included"></a>包含的内容
 
 安装 Microsoft R Server 时，所获得的增强 R 包和连接工具与 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]的选项。 所有 Microsoft R Server 部署包含 R 基础包，以及一组用于支持并行处理、改进性能及与数据源（包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Hadoop）建立连接的增强 R 包。
 
 不需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。 使用本地计算上下文和 Microsoft R Server（独立版）运行 R 代码时，将使用 R 脚本自身的 R 二进制文件集和包库执行该脚本。 
 若要在数据库内运行代码，请将解决方案部署到 SQL Server，或使用远程计算上下文。  

  
### <a name="r--packages"></a>R 包 
  
R 库安装在用于安装的 SQL Server 版本关联的文件夹中。 在此文件夹中，还可以找到示例数据、R 基础包的文档以及 R 工具和运行时的文档。  

**使用 SQL Server 2016 安装 R Server（独立版）**  
`C:\Program Files\Microsoft SQL Server\130\R_SERVER`         

**使用 SQL Server 2017 安装 R Server（独立版）**  
`C:\Program Files\Microsoft SQL Server\140\R_SERVER`   
       
**使用独立的 Windows 安装程序安装 R Server（独立版）**     
`C:\Program Files\Microsoft\R Server\R_SERVER`
      
> [!IMPORTANT]  
>  如果在同一台计算机上安装了带有 R Services（数据库内）的 SQL Server 实例，则 R 库和工具安装在另一个文件夹中：  `C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES`  
>   
>  不要直接调用与 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例关联的 R 包或实用工具。 如果 R Server 和 R Services 安装在同一台计算机上，请始终使用 R_SERVER 文件夹中的 R 工具和包。 

  
### <a name="r--tools"></a>R 工具  
  
安装过程中不会安装 R 开发 IDE。 不需要使用其他工具，因为所有标准基础 R 工具都包含在 `C:\Program Files\Microsoft SQL Server\130\R_SERVER\bin` 中。  
  
但是，我们建议安装 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 或你偏好的其他开发环境，例如 RStudio。 有关详细信息，请参阅[安装或配置 R 工具](../../advanced-analytics/r-services/setup-or-configure-r-tools.md)或 [RTVS 入门](http://rtvs/)。  


## <a name="troubleshooting"></a>故障排除  

### <a name="incompatible-version-of-r-client-and-r-server"></a>R Client 与 R Server 的版本不兼容

如果安装最新版本的 Microsoft R Client，并使用它在远程计算机环境中的 SQL Server 上运行 R，则可能收到以下错误：

计算机上运行的 Microsoft R Client 版本为 9.0.0，与 8.0.3 版的 Microsoft R Server 不兼容。请下载并安装兼容版本。

通常情况下，随 SQL Server R Services 一起安装的 R 版本会在发布 Service Release 后进行更新。 若要确保始终拥有最新版本的 R 组件，请安装所有 Service Pack。 为了与 Microsoft R Client 9.0.0 兼容，必须安装本 [支持文章](https://support.microsoft.com/kb/3210262)中介绍的更新。 


### <a name="installing-microsoft-r-server-on-an-instance-of-sql-server-installed-on-windows-core"></a>在 Windows Core 上安装的 SQL Server 实例上安装 Microsoft R Server
在 SQL Server 2016 发布版本中，将 Microsoft R Server 添加到 Windows Server Core 版本上的实例时有一个已知问题。 此问题已解决。 

如果遇到此问题，可以应用 [KB3164398](https://support.microsoft.com/kb/3164398) 中介绍的解决方法向 Windows Server Core 上的现有实例添加 R 功能。   有关详细信息，请参阅 [不能在 Windows Server Core 操作系统上安装 Microsoft R Server 独立版](https://support.microsoft.com/kb/3168691)。


###  <a name="bkmk_Uninstall"></a> Upgrading from an Older Version of Microsoft R Server  
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
  
  

