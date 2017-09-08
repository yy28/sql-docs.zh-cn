---
title: "在 Azure 上预配 R Server Only SQL Server 2016 Enterprise VM | Microsoft Docs"
ms.custom: 
ms.date: 06/05/2017
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
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a3bfca0753984f09220d8ca4e4f6933c949daf2b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="advanced-analytics-virtual-machines-on-azure"></a>高级的分析在 Azure 上的虚拟机

在 Azure 上的虚拟机是一个方便的选项，用于快速配置用于机器学习解决方案的完整的服务器环境。 本主题列出了包含 R Server、 SQL Server 使用机器学习中或从 Microsoft 其他数据科学工具某些虚拟机映像。

> [!TIP]
> 我们建议你使用 Azure 门户和 Azure 应用商店的新版本。 在浏览经典门户上的 Azure 库时，某些图像不可用。

Azure 应用商店包含支持数据科学的多个虚拟机。 此列表不完整，但仅提供了包含学习服务，为了便于发现的 Microsoft R Server 或 SQL Server 计算机的映像的名称。

## <a name="how-to-provision-a-vm"></a>如何设置虚拟机

如果你不熟悉如何使用 Azure Vm，我们建议你看到这些文章以获取有关使用门户和配置虚拟机的详细信息。

+ [虚拟机 - 入门](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)
+ [开始使用 Windows 虚拟机](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-hero-tutorial/)

### <a name="find-an-image"></a>查找映像

1. 从 Azure 仪表板，单击**Marketplace**。

    - 单击**智能和分析**或**数据库**，然后键入"R"**筛选器**控件以查看 R Server 虚拟机的列表。
    - 其他可能字符串**筛选器**控件*数据科学*和*机器学习*
    - 在搜索中使用 %通配符来查找包含目标字符串，如的 VM 名称*R*或*Julia*。

2. 若要获取 R Server for Windows，请选择**R Server 仅 SQL Server 2016 Enterprise**。
  
    [R Server](https://msdn.microsoft.com/microsoft-r/rserver-whats-new)被许可为 SQL Server 企业版功能，但版本 9.1。 安装为独立服务器和现代生命周期支持策略下提供服务。

3. 虚拟机已创建并运行之后，单击“连接”按钮以打开连接并登录到新计算机。

4. 连接后，你可能需要安装其他 R 工具或开发工具。

### <a name="install-additional-r-tools"></a>安装其他 R 工具

默认情况下，Microsoft R Server 包含随 R 的基础安装而安装的所有 R 工具（包括 RTerm 和 RGui）。 如果要立即开始使用 R，则 RGui 的快捷方式已添加到桌面。

但是，你可能想要安装其他 R 工具，如 RStudio、 R Tools for Visual Studio (RTVS) 或 Microsoft R 客户端。 请参阅以下链接以了解下载位置和说明：
+ [R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)
+ [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/install-r-client-windows)
+ [RStudio for Windows](https://www.rstudio.com/products/rstudio/download/)

安装完成后，请务必更改默认 R 运行时位置，以便所有 R 开发工具使用 Microsoft R Server 库。

### <a name="configure-server-for-web-services"></a>配置 web 服务的服务器

如果虚拟机包含 R Server，则需要完成额外的配置才能使用 Web 服务部署、远程执行，或者在组织中使用 R Server 作为部署服务器。 有关说明，请参阅 [Configure R Server for Operationalization](https://msdn.microsoft.com/microsoft-r/operationalize/configuration-initial)（为操作化配置 R Server）。

> [!NOTE]
> 如果你只是想要使用如 RevoScaleR 或 MicrosoftML 的包，则不需要其他配置。

## <a name="r-server-images"></a>R Server 映像

### <a name="microsoft-data-science-virtual-machine"></a>Microsoft 数据科学虚拟机

来自配置与 Microsoft R Server，以及 Python （Anaconda 分发）、 Jupyter 笔记本 server、 Visual Studio Community Edition、 Power BI Desktop、 Azure SDK 和 SQL Server Express 版本。

Windows 版本 Windows Server 2012 上运行，并包含许多建模和分析，包括 CNTK 和 mxnet、 流行的 R 包，如 xgboost 和 Vowpal Wabbit 的特殊工具。

### <a name="linux-data-science-virtual-machine"></a>Linux 数据科学虚拟机

此外包含用于数据科学和开发活动，包括 Microsoft R Open、 Microsoft R Server Developer Edition、 Anaconda Python 和 Jupyter 笔记本 Python、 R 和 Julia 的常用工具。

此 VM 映像最近已更新为包括 JupyterHub，可以通过不同的身份验证方法，包括本地操作系统帐户身份验证和 Github 帐户身份验证进行多个用户使用的开放源代码软件。 如果你想要运行的定型类，并且希望所有学生共享相同的服务器，但使用单独的笔记本和目录，JupyterHub 是一个特别有用的选项。

针对 Ubuntu、 Centos 和 Centos CSP 提供映像。

### <a name="r-server-only-sql-server-2016-enterprise"></a>R Server 仅 SQL Server 2016 Enterprise

此虚拟机包括独立安装程序[R Server 9.1。](https://msdn.microsoft.com/microsoft-r/rserver-whats-new) 支持新的现代软件生命周期授权模型。

 R Server 也会为 Linux CentOS 版本 7.2，Linux RedHat 版本 7.2 和 Ubuntu 版本 16.04 映像中提供。

 > [!NOTE]
 > 这些虚拟机替换了以前在 Azure 应用商店中提供的 **Windows 虚拟机的 RRE**。

## <a name="sql-server-images"></a>SQL Server 映像

若要使用 R Services （数据库） 或机器学习服务，必须安装一个 SQL Server Enterprise 或开发人员版虚拟机，并添加机器学习服务，如下所述：[安装上的 SQL Server R ServicesAzure 虚拟机](../../advanced-analytics/r-services/installing-sql-server-r-services-on-an-azure-virtual-machine.md)。

> [!NOTE]
> 目前，在 Linux 虚拟机上或在 Azure SQL 数据库的 SQL Server 自 2017 年，不支持机器学习服务。 适用于 Windows，你必须使用 SQL Server 2016 SP1 或 SQL Server 自 2017 年。

数据科学虚拟机还包括与已启用了 R 服务功能的 SQL Server 2016。


## <a name="other-vms"></a>其他 Vm

### <a name="deep-learning-toolkit-for-the-data-science-virtual-machine"></a>深层数据科学虚拟机的学习工具包

此虚拟机包含相同的机器学习工具可用在数据科学虚拟机上，但与 mxnet、 CNTK、 TensorFlow，和 Keras GPU 版本。 仅在 Azure 的 GPU N 系列实例上，可以使用此映像。 

深入学习工具包还提供一套深入学习使用 GPU，包括 CIFAR 10 数据库上的图像识别和字符识别示例 MNIST 数据库上的解决方案的示例。 GPU 实例都是在美国中南部、 美国东部、 欧洲西部和亚洲东南部当前可用的。

> [!IMPORTANT]
> GPU 实例目前仅在美国中南部提供。


## <a name="frequently-asked-questions"></a>常见问题

### <a name="can-i-install-a-virtual-machine-with-sql-server-2017"></a>可以使用 SQL Server 2017 安装虚拟机？

映像可用包含 SQL Server 自 2017 年 1 CTP 2.0 为 Linux 环境，但这些环境中当前不支持机器学习服务。 

基于 Windows 的虚拟机的 SQL Server 自 2017 年 1 Enterprise Edition 包含机器学习服务将公开发布的版本后可用。 

作为替代方法，你可以使用 SQL Server 2016 映像，并升级你的 R 实例，如下所述：[升级实例使用 SqlBindR](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。 

或者，创建虚拟机和下载 CTP 2.0 预览版的[SQL Server 2017](https://www.microsoft.com/sql-server/sql-server-2017)。

### <a name="how-do-i-access-data-in-an-azure-storage-account"></a>如何访问 Azure 存储帐户中的数据？

需要使用 Azure 存储帐户中的数据时，有几个选项可用于访问或移动数据：

+ 使用实用工具（如 [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only)）将数据从存储帐户复制到本地文件系统。 

+ 将文件添加到存储帐户上的文件共享，然后在 VM 上以网络驱动器的形式装载文件共享。  有关详细信息，请参阅 [装载 Azure 文件](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/)。 

### <a name="how-do-i-use-data-from-azure-data-lake-storage-adls"></a>如何使用 Azure Data Lake Storage (ADLS) 中的数据？

如果引用相同的方式将 HDFS 文件系统，通过使用 webHDFS 的存储帐户，你可以从使用 RevoScaleR，ADLS 存储读取数据。  有关详细信息，请参阅此文章：[使用 R 来执行 Azure Data Lake 存储上的文件系统操作](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/03/14/using-r-to-perform-filesystem-operations-on-azure-data-lake-store/)。

## <a name="see-also"></a>另请参阅

[SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx)


