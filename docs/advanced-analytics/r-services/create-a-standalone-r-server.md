---
title: "创建 R Server（独立版） | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 408e2503-5c7d-4ec4-9d3d-bba5a8c7661d
caps.latest.revision: 35
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 27
---
# 创建 R Server（独立版）
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序包含用于安装 **Microsoft R Server（独立版）**的选项。 使用此选项，可在连接到所选数据库或数据源时在 Windows 上开发高性能 R 解决方案。 Microsoft R Server 仅在 Enterprise Edition 中可用  
  
 安装 Microsoft R Server 时，所获得的增强 R 包和连接工具与 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中提供的相同，但不需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例，并且是在独立计算机上（而非数据库中）执行 R 脚本。  
  
> [!NOTE]  
>  现在还可以通过简化的安装程序安装 Microsoft R Server，该安装程序在[现代生命周期](https://support.microsoft.com/help/447912)策略中注册实例。 此支持产品/服务可确保用户始终使用 R 的最新版本。若要深入了解如何使用简化的安装程序，请参阅[运行 Microsoft R Server for Windows](https://msdnstage.redmond.corp.microsoft.com/microsoft-r/rserver-install-windows?branch=r-server-nov16-dev)。
>  
> 如果通过简化的安装程序安装 Microsoft R Server，还可以将指定的任何 R Services 实例转换为使用新的支持策略并获取更频繁的 R 组件更新。有关详细信息，请参阅[使用 sqlBindR.exe 升级 R Services 的实例](http://www.bing.com)。   
  
##  <a name="a-namebkmkinstallrservicesindatabasea-install-microsoft-r-server-standalone"></a><a name="bkmk_installRServicesInDatabase"></a>安装 Microsoft R Server（独立版）  
  
1.  如果已安装早期版本的 Microsoft R Server，必须先卸载它。  请参阅[从 Microsoft R Server 的旧版本升级](#bkmk_Uninstall)。 

2. 运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序。  
  
2.  在“安装”  选项卡上，单击“新的 R Server（独立版）安装”  。  
  
     ![Setup option for R Server Standalone](../../advanced-analytics/r-services/media/rsql-rstandalonesetup.png "Setup option for R Server Standalone")  
  
3.  在“功能选择”  页上，应已选择以下选项：  
  
    -   **R Server（独立版）**  
  
         此选项将安装共享功能，包括开放源代码 R 工具和基础包，以及 Microsoft R 提供的增强 R 包和连接工具。  
  
     应忽略所有其他选项。  
  
4.  接受下载和安装 Microsoft R Open 的许可条款。 当“接受”按钮变为不可用时，可以单击“下一步”。 安装这些组件（以及它们可能需要的任何必备项）可能需要花费一些时间。   
  
5.  在“准备安装”  页上，验证选择，并单击“安装”。  
  
> [!TIP]
> 有关自动安装或脱机安装的详细信息，请参阅[从命令行安装 Microsoft R Server](../../advanced-analytics/r-services/install-microsoft-r-server-from-the-command-line.md)。

  
## <a name="what-is-installed-and-where-to-find-r-packages"></a>安装的内容以及在何处查找 R 包  
 Microsoft R Server 包含 R 基础包和一组增强的 R 包，支持并行处理、改进了性能并可连接数据源（包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 Hadoop）。  
  
-   **R 包**  
  
     R 库与随 Microsoft SQL Server 2016 安装的其他工具和实用程序一起安装。 例如：  
  
     `C:\Program Files\Microsoft SQL Server\130\R_SERVER`  
  
     此外，在此文件夹中可以找到 R 基础包文档、示例数据以及 R 工具和运行时文档。  
  
    > [!NOTE]  
    >  如果在同一台计算机上安装了带有 R Services（数据库内）的 SQL Server 实例，则 R 库和工具安装在另一个文件夹中：`C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES`  
    >   
    >  不要使用与 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例关联的 R 包或实用程序。 始终使用 R_SERVER 文件夹中的 R 工具和包。  
  
-   **R 工具**  
  
     安装过程中不会安装 R 开发 IDE。 可以安装 RStudio、[!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 或喜欢的其他任何开发环境。  
  
     但是，不需要其他工具。 `C:\Program Files\Microsoft SQL Server\130\R_SERVER\bin` 中包含所有标准的 R 基础工具。  
  
     有关详细信息，请参阅[安装或配置 R 工具](../../advanced-analytics/r-services/setup-or-configure-r-tools.md)。  


 
## <a name="troubleshooting"></a>故障排除  

### <a name="incompatible-version-of-r-client-and-r-server"></a>R Client 与 R Server 的版本不兼容

如果安装最新版本的 Microsoft R Client，并使用它在远程计算机环境中的 SQL Server 上运行 R，则可能收到以下错误：

计算机上运行的 Microsoft R Client 版本为 9.0.0，与 8.0.3 版的 Microsoft R Server 不兼容。请下载并安装兼容版本。

通常情况下，随 SQL Server R Services 一起安装的 R 版本会在发布 Service Release 后进行更新。 若要确保始终拥有最新版本的 R 组件，请安装所有 Service Pack。 为了与 Microsoft R Client 9.0.0 兼容，必须安装本[支持文章](https://support.microsoft.com/kb/3210262)中介绍的更新。 


### <a name="installing-microsoft-r-server-on-an-instance-of-sql-server-installed-on-windows-core"></a>在 Windows Core 上安装的 SQL Server 实例上安装 Microsoft R Server
在 SQL Server 2016 发布版本中，将 Microsoft R Server 添加到 Windows Server Core 版本上的实例时有一个已知问题。 此问题已解决。 

如果遇到此问题，可以应用 [KB3164398](https://support.microsoft.com/kb/3164398) 中介绍的解决方法向 Windows Server Core 上的现有实例添加 R 功能。   有关详细信息，请参阅[不能在 Windows Server Core 操作系统上安装 Microsoft R Server 独立版](https://support.microsoft.com/kb/3168691)。


###  <a name="a-namebkmkuninstalla-upgrading-from-an-older-version-of-microsoft-r-server"></a><a name="bkmk_Uninstall"></a>从 Microsoft R Server 的旧版本升级  
 如果安装了 Microsoft R Server 的预发布版本，必须先卸载它，才能升级到较新版本。  
  
**卸载 R Server（独立版）**  
  
1.  在“控制面板”中，单击“添加或删除程序”，然后选择 `Microsoft SQL Server 2016 <version number>`。  
  
2.  在具有“添加”、“修复”或“删除”组件选项的对话框中，选择“删除”。  
  
3.  在“选择功能”页面上的“共享功能”下，选择“R Server（独立版）”。 单击“下一步”，然后单击“完成”，卸载所选组件。  
   
### <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>安装失败，显示错误：“一次只能安装一个 Revolution Enterprise 产品”。  
如果安装了较老的 Revolution Analytics 产品或 SQL Server R Services 的预发行版本，可能会遇到此错误。 安装较新版本的 Microsoft R Server 之前，必须先卸载任何以前的版本。 不支持与其他版本的 Revolution Enterprise 工具一起并行安装。  

但是，如果配合使用 R Server 独立版和 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]，则支持并行安装。 
  
### <a name="unable-to-uninstall-older-components"></a>无法卸载较旧的组件   
  
如果删除较旧版本时遇到问题，可能需要编辑注册表以删除相关项。  

> [!IMPORTANT]
> 此问题仅在安装了预发布版 Microsoft R Server 或 CTP 版 SQL Server 2016 R Services 时才出现。
  
1. 打开 Windows 注册表，并找到此项：`HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`。  
2. 如果存在以下条目且项仅包含值 `sEstimatedSize2`，请删除这些条目：  
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972（针对 8.0.2）  
  
    -   46695879-954E-4072-9D32-1CC84D4158F4（针对 8.0.1）  
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B（针对 8.0.0）  
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A（针对 7.5.0）  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft R Server](../../advanced-analytics/r-services/r-server-standalone.md)  
  
  