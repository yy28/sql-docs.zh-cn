---
title: "在 Azure 上预配 R Server Only SQL Server 2016 Enterprise VM | Microsoft Docs"
ms.custom: 
ms.date: 12/22/2016
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c8826df7-aa67-4768-baa9-bdc875c4a766
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 708a03256a9308aaab150a20915e14f35fe4049a
ms.lasthandoff: 04/11/2017

---
# <a name="provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure"></a>在 Azure 上预配 R Server Only SQL Server 2016 Enterprise VM
使用 Azure 上的虚拟机可以快速方便地为 R 解决方案配置完整的服务器环境。 

Azure 应用商店中提供多个支持数据科学且包含 Microsoft R Server 的虚拟机：

+ **Microsoft 数据科学虚拟机**配置了 Microsoft R Server、Python（Anaconda 分发版）、Jupyter Notebook 服务器、Visual Studio Community Edition、Power BI Desktop、Azure SDK 和 SQL Server Express Edition。 

+ **Linux 数据科学虚拟机**也包含 Microsoft R Server，以及 Weka、PySpark Jupyter 支持和用于深度学习的 mxnet。

+ **Microsoft R Server 2016 for Linux** 包含最新版本的 R Server（版本 9.0.1）。 针对 CentOS 版本 7.2 和 Ubuntu 版本 16.04 提供单独的 VM。 

+ **R Server Only SQL Server 2016 Enterprise** 虚拟机包含 [R Server 9.0.1](https://msdn.microsoft.com/microsoft-r/rserver-whats-new) 的独立安装程序，支持全新的现代软件生命周期授权模型。 

> [!NOTE]
> 这些虚拟机替换了以前在 Azure 应用商店中提供的 **Windows 虚拟机的 RRE**。
> 
>本文中的说明取代了以前适用于包含 DeployR 功能的“R Server Only SQL Server 2016 Enterprise”版本 (8.0.3) 的说明。 如果你已安装 8.0.3 VM，可在 MSDN 上的 [Provision version 8.0.3 R Server (standalone) SQL Server 2016 Enterprise feature](https://msdn.microsoft.com//microsoft-r/rserver-install-windows-vm803provisioning)（预配 8.0.3 版 R Server（独立版）SQL Server 2016 功能）中找到预配说明。


## <a name="provision-a-virtual-machine-with-r-and-sql-server"></a>使用 R 和 SQL Server 预配虚拟机

如果你刚接触 Azure VM 的使用，则我们建议查看本文以了解有关使用门户和配置虚拟机的详细信息。
[虚拟机 - 入门](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)

### <a name="to-create-an-r-server-virtual-machine-from-the-microsoft-azure-marketplace"></a>通过 Microsoft Azure 应用商店创建 R Server 虚拟机 
1. 单击“虚拟机”，然后在搜索框中输入 R Server。
2. 选择包含 Microsoft R Server 的虚拟机之一。 

      + 若要获取 Microsoft R Server for Windows，请选择“R Server Only SQL Server 2016 Enterprise”。 [R Server for Windows 版本 9.0.1](https://msdn.microsoft.com/microsoft-r/rserver-whats-new) 以 SQL Server Enterprise 功能的形式授权，但版本 9.0.1 作为独立的服务器安装，根据新式软件生命周期策略而不是 SQL Server 支持提供服务。
      + 若要使用 SQL Server R Services，必须根据以下文章中所述安装 SQL Server 2016 Enterprise 或 Developer 版本的虚拟机之一：[Installing SQL Server R Services on an Azure Virtual Machine](../../advanced-analytics/r-services/installing-sql-server-r-services-on-an-azure-virtual-machine.md)（在 Azure 虚拟机上安装 SQL Server R Services）。

3. 按照以下文章中所述继续设置虚拟机： [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-hero-tutorial/) 
7. 虚拟机已创建并运行之后，单击“连接”按钮以打开连接并登录到新计算机。
8. 进行连接时，“服务器管理器”会在默认情况下打开，但无需其他服务器配置。 关闭“服务器管理器”以访问桌面，并继续进行后续步骤：
    + 安装其他 R 工具或开发工具
    + 操作化 R Server

### <a name="to-locate-the-r-server-vm-in-the-azure-classic-portal"></a>在 Azure 经典门户中查找 R Server VM
1. 单击“虚拟机”，然后单击“新建”。
2. 在“新建”窗格中，“计算”和“虚拟机”应该已处于选择状态。 
3. 单击“从库中”以查找 VM 映像。 可以在搜索框中输入 R Server 或单击“Microsoft”，然后向下滚动，直到看到“R Server Only SQL Server 2016 Enterprise”。


## <a name="install-r-tools"></a>安装 R 工具
默认情况下，Microsoft R Server 包含随 R 的基础安装而安装的所有 R 工具（包括 RTerm 和 RGui）。 如果要立即开始使用 R，则 RGui 的快捷方式已添加到桌面。

但是，你可能希望在 Visual Studio 2015 或 Microsoft R Client 中安装其他 R 工具，例如 RStudio、用于 Visual Studio 的 R 工具 (RTVS) 加载项。 请参阅以下链接以了解下载位置和说明：
+ [Visual Studio 2015](https://www.visualstudio.com/downloads/) 和[用于 Visual Studio 的 R 工具](https://www.visualstudio.com/features/rtvs-vs.aspx)
+ [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/install-r-client-windows)
+ [RStudio for Windows](https://www.rstudio.com/products/rstudio/download/)

安装完成后，请务必更改默认 R 运行时位置，以便所有 R 开发工具使用 Microsoft R Server 库。

## <a name="operationalize-r-server-for-windows-on-the-virtual-machine"></a>在虚拟机上操作化 R Server for Windows

如果虚拟机包含 R Server，则需要完成额外的配置才能使用 Web 服务部署、远程执行，或者在组织中使用 R Server 作为部署服务器。 如果想要在版本 9.0.1 中使用新 [mrsdeploy 包](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy)中的功能，则必须执行此步骤。

有关说明，请参阅 [Configure R Server for Operationalization](https://msdn.microsoft.com/microsoft-r/operationalize/configuration-initial)（为操作化配置 R Server）。

> [!NOTE]
> 仅当你要使用 mrsdeploy 或者[操作化 R Server](https://msdn.microsoft.com/microsoft-r/operationalize/about) 中所述的其他功能时，才需要完成额外的配置。 使用 ReovScaleR、用于机器学习集成的 MicrosoftML、olapR 或 Microsoft R 专有的其他 R 包不需要执行此步骤。 

## <a name="frequently-asked-questions"></a>常见问题解答

### <a name="how-do-i-access-data-in-an-azure-storage-account"></a>如何访问 Azure 存储帐户中的数据？

需要使用 Azure 存储帐户中的数据时，有几个选项可用于访问或移动数据：

+ 使用实用工具（如 [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only)）将数据从存储帐户复制到本地文件系统。 

+ 将文件添加到存储帐户上的文件共享，然后在 VM 上以网络驱动器的形式装载文件共享。  有关详细信息，请参阅 [装载 Azure 文件](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/)。 

### <a name="how-do-i-use-data-from-azure-data-lake-storage-adls"></a>如何使用 Azure Data Lake Storage (ADLS) 中的数据？

如果采用与用于 HDFS 文件系统（使用 webHDFS）的相同方式来引用存储帐户，则可以使用 ScaleR 从 ADLS 存储读取数据。  有关详细信息，请参阅此 [设置指南](http://go.microsoft.com/fwlink/?LinkId=723452)。

### <a name="which-virtual-machine-is-best-for-me"></a>哪个虚拟机最适合我？

Azure 门户提供了多个包含 Microsoft R Server 的虚拟机映像。 请使用包含所需工具的虚拟机。

**数据科学虚拟机**

在 Windows Server 2012 上运行。 包含以下用于数据科学建模和开发活动的工具：
- Microsoft R Server Developer Edition [版本 9.0.1](https://msdn.microsoft.com/microsoft-r/rserver-whats-new)
- Anaconda Python 发行版
- 适用于 Python 和 R 的 Jupyter 笔记本
- 包含 Python、R 和 node.js 工具的 Visual Studio Community Edition
- Power BI Desktop
- SQL Server 2016 Developer Edition
- CNTK（Microsoft 开发的开源深度学习工具包）
- mxnet
- xgboost 等机器学习算法
- Vowpal Wabbit

VM 上的 Azure SDK 和库可让你使用云中属于 Cortana Analytics Suite 的各种服务（包括 Azure 机器学习、Azure 数据工厂、流分析和 SQL 数据仓库、Hadoop、Data Lake、Spark 等）构建应用程序。

**用于数据科学虚拟机的深度学习工具包**

除了数据科学虚拟机上的功能以外，还包括：
- 深度学习工具包 
- GPU 版本的 mxnet 和 CNTK，用于 Azure GPU N 系列实例
- 使用 GPU 的示例深度学习解决方案，包括 CIFAR-10 数据库中的映像识别，以及 MNIST 数据库中的字符识别示例

GPU 使用离散设备分配，非常适合用于解决需要大型训练集和代价不菲的计算训练工作的深度学习问题。  

> [!IMPORTANT]
> GPU 实例目前仅在美国中南部提供。

**Linux 数据科学虚拟机**

有两个 Linux 虚拟机，一个基于 Openlogic CentOS，另一个基于 Ubuntu。 此虚拟机包含以下用于开发和数据科学的工具：


- Microsoft R Server Developer Edition [版本 9.0.1](https://msdn.microsoft.com/microsoft-r/rserver-whats-new)
- Anaconda Python 发行版
- 适用于 Python、R 和 Julia 的 Jupyter 笔记本
- Postgres 数据库的本地实例
- Azure 命令行工具
- 用于 Python、R、Java、node.js、Ruby、PHP 的 Azure SDK
- 用于 Ruby、PHP、node.js、Java、Perl、Eclipse 的运行时
- vim、Emacs 和 gedit 等标准编辑器
- 用于访问各种 Azure 服务的库 
- CNTK（Microsoft Research 开发的深度学习工具包）
- Vowpal Wabbit 
- xgboost

你对虚拟机和 shell 拥有完全访问权限，包括对预配 VM 期间创建的帐户的 *sudo* 访问权限。 

JupyterHub 已在虚拟机上预先配置。 它为 Python、Julia 和 R 提供基于浏览器的试验和开发环境。 

另外，虚拟机上还预先配置了远程图形桌面。 在 X2Go 客户端上需要执行一些附加的步骤。 

### <a name="where-can-i-find-more-information"></a>在哪里可以找到详细信息？

在 MSDSN 库中可以找到有关 Microsoft R 的其他文档：[R Server 和 ScaleR](https://msdn.microsoft.com/microsoft-r)  

若要大致了解 R，请参阅以下资源： 
+ [DataCamp](http://www.datacamp.com) - 提供 R 的免费初级和中级课程，以及有关使用 Revolution R 处理大数据的课程。
+ [Stack Overflow](http://www.stackoverflow.com) - 适用于 R 编程和 ML 工具问题的极佳资源。 
+ [Cross Validated](https://stats.stackexchange.com/) - 针对机器学习中统计问题的相关问题的站点。
+ [R 帮助邮件列表存档](https://www.r-project.org/mail.html)和 [MRAN 网站](https://mran.microsoft.com/documents/getting-started/) - 有关历史信息（例如存档的问题）的极佳资源 


## <a name="see-also"></a>另请参阅
[SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx)


