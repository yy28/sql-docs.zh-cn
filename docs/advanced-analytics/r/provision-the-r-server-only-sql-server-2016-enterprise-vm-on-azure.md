---
title: "设置用于在 Azure 上的机器学习的虚拟机 |Microsoft 文档"
ms.custom: 
ms.date: 10/16/2017
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
ms.sourcegitcommit: 8cc1fcfdeae8742a93916dfb08c9db1215f88721
ms.openlocfilehash: 7cb9e069fc3b537f8aab9d048a152435ad0cc6ac
ms.contentlocale: zh-cn
ms.lasthandoff: 10/17/2017

---
# <a name="provision-a-virtual-machine-for-machine-learning-on-azure"></a>设置用于在 Azure 上的机器学习的虚拟机

在 Azure 上的虚拟机是一个方便的选项，用于快速配置用于机器学习解决方案的完整的服务器环境。 本文列出了一些使用机器学习中包含 R Server、 机器学习的服务器或 SQL Server 的虚拟机映像。

此列表不完整，但仅提供了与计算机学习服务器或 SQL Server 计算机学习 Services，为了便于发现相关的映像的名称。

> [!TIP]
> 我们建议你使用 Azure 门户和 Azure 应用商店的新版本。 在浏览经典门户上的 Azure 库时，某些图像不可用。

## <a name="how-to-provision-a-virtual-machine"></a>如何设置虚拟机

如果你不熟悉如何使用 Azure Vm，我们建议你看到这些文章以获取有关使用门户和配置虚拟机的详细信息。

+ [虚拟机 - 入门](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)
+ [开始使用 Windows 虚拟机](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/)

## <a name="find-a-machine-learning-image"></a>找到机器学习映像

1. 从 Azure 门户 (portal.azure.com) 中，单击**虚拟机**，或单击**新建**。

2. 找到在页上，可用于按名称筛选资源顶部的搜索框。 

3. 键入"R Server"（或"ML 服务器"）**筛选器**控件以查看相关资源的列表。 单击**在应用商店中的搜索**以查看虚拟机。

    > [!TIP]
    > 
    > 筛选器控件的其他可能字符串是"数据科学"和"机器学习"。
    > 
    > 使用`%`搜索以查找虚拟机的名称中的通配符。 例如，你可以键入`"`%julia%` or `%R %。

4. 若要获取 R Server for Windows，请选择**R Server 仅 SQL Server 2016 Enterprise**。
  
    [R Server](https://msdn.microsoft.com/microsoft-r/rserver-whats-new)许可作为 SQL Server 企业版功能，但已安装为独立的服务器版本 9.1，现代生命周期支持策略下已得到处理。

    > [!NOTE] 
    > 
    > 这在查找版的新的虚拟机，其中包括 SQL Server 2017 和 9.2.1 的机器学习 Server 版本。
    > 到那时，你可以更新通过使用 SQL Server 安装中心，并选择升级选项在此虚拟机上安装的 SQL Server 的版本。 有关详细信息，请参阅[使用安装向导升级 SQL Server](https://docs.microsoft.com/sql/database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup)。

5. 虚拟机已创建并运行后，单击**连接**按钮以打开连接并登录到新计算机。

5. 连接后，你可以安装其他 R 包或你首选的开发工具。

### <a name="install-additional-r-tools"></a>安装其他 R 工具

默认情况下，Microsoft R Server 包含随 R 的基础安装而安装的所有 R 工具（包括 RTerm 和 RGui）。 RGui 的快捷方式也已添加到桌面。

但是，你可能想要安装其他 R 工具，如 RStudio、 R Tools for Visual Studio (RTVS) 或 Microsoft R 客户端。 请参阅以下链接以了解下载位置和说明：

+ [R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)
+ [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/install-r-client-windows)
+ [RStudio for Windows](https://www.rstudio.com/products/rstudio/download/)

安装完成后，请务必更改默认 R 运行时位置，以便所有 R 开发工具使用 Microsoft R Server 库。

### <a name="configure-r-server-to-support-web-services"></a>R 将服务器配置为支持 web 服务

若要使用 web 服务部署，远程执行，或为你的组织中的部署服务器利用 R Server 需要其他配置。 有关说明，请参阅[配置 R 服务器具有可操作性分析](https://docs.microsoft.com/machine-learning-server/install/operationalize-r-server-one-box-config)。

> [!NOTE]
> 如果你只是想要使用如 RevoScaleR 或 MicrosoftML 的包，则不需要其他配置。

## <a name="other-virtual-machines"></a>其他虚拟机

以下映像可从 Azure 应用商店，包括完全配置机器学习工具，但不是一定包含 SQL Server。

### <a name="data-science-virtual-machine"></a>数据科学虚拟机

此映像预先配置为使用 Microsoft R Server，以及 Python （Anaconda 分发）、 Jupyter 笔记本 server、 Visual Studio Community Edition、 Power BI Desktop、 Azure SDK 和 SQL Server Express 版本。

Windows 版本在 Windows Server 2012 上运行，并且包含适用于建模和分析，包括许多特殊工具[CNTK](https://www.microsoft.com/cognitive-toolkit/)， [mxNet](https://mxnet.incubator.apache.org/)，和受欢迎的 R 包**xgboost**.

Linux 版本供 Ubuntu、 Centos 和 Centos CSP，并包含用于数据科学和开发活动的许多常用工具。

有关详细信息，请参阅[适用于 Linux 和 Windows 的介绍与 Azure 数据科学虚拟机](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/provision-vm)。

此映像最近已更新为包括： 

+ Julia，将来的可缩放的、 功能强大的数据科学语言的支持 
+ JupyterHub，如果你想要运行的定型类，并且希望所有学生共享相同的服务器，但使用单独的笔记本和目录是一个有用的选项。

有关支持的工具和机器学习框架的详细信息，请参阅[了解你的数据科学虚拟机](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/dsvm-tools-overview)

### <a name="r-server-virtual-machines"></a>R Server 虚拟机

除了**R Server 仅 SQL Server 2016 Enterprise**映像，你可以获取包含 R Server 的独立虚拟机。 映像是可用于 Linux CentOS 版本 7.2、 Linux RedHat 版本 7.2 和 Ubuntu 版本 16.04。

有关详细信息，请参阅[云中的机器学习服务器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-in-the-cloud)

 > [!NOTE]
 > 这些虚拟机替换了以前在 Azure 应用商店中提供的 **Windows 虚拟机的 RRE**。

### <a name="sql-server-virtual-machines"></a>SQL Server 虚拟机

有为使用 SQL Server 机器学习在 Azure 中的两个选项：

+ 获取包含预装 SQL Server R Services 的虚拟机映像之一。
+ 创建 Azure 虚拟机并安装 SQL Server Enterprise 或开发人员使用你自己的许可证密钥的版本。 
  
    然后，再次运行安装程序将添加并启用机器学习服务，如下所述：[安装 Azure 虚拟机上 SQL Server R Services](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)。
+ 创建 Azure SQL 数据库使用可以支持机器学习中，并使用新的 R 服务功能当前在预览版中的服务层。 有关详细信息，请参阅[Azure SQL DB](../r/using-r-in-azure-sql-database.md)。

> [!NOTE]
> 目前，SQL Server 计算机学习 Services 不支持的 Linux 虚拟机上的 SQL Server 自 2017 年。 但是，你可以执行使用 T-SQL 的预测函数的训练模型评分。 有关详细信息，请参阅[SQl Server 中的本机评分](../sql-native-scoring.md)。 

### <a name="virtual-machines-for-deep-learning"></a>深入学习的虚拟机 

以前，Microsoft 提供深层学习工具包供数据科学虚拟机，你无法将其添加到现有数据科学虚拟机。 该工具包现在取代深入学习的虚拟机，其中包含常用的深入学习工具：

+ GPU 版本的深入学习框架，如 Microsoft 认知工具包、 TensorFlow、 Keras 和 Caffe
+ 内置 GPU 驱动程序
+ 适用于图像和文本处理工具的集合
+ 企业开发工具如 Microsoft R Server Developer Edition，Anaconda Python，Python 和 R 的 Jupyter 笔记本
+ 用于 Python、 R、 SQL Server 和其他更多的开发人员工具
+ 图像和文本理解的端到端示例

深入学习虚拟机是在 Windows 2016 或 Ubuntu Linux 平台上可用。 有关详细信息，请参阅[深入学习和 AI 框架](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/dsvm-deep-learning-ai-frameworks)。

> [!IMPORTANT]
> 
> 部署此虚拟机需要 Azure GPU NC 系列虚拟机映像，这两项在有限的 Azure 区域可用。 有关可用性的信息，请参阅[按区域可用的产品](https://azure.microsoft.com/en-us/regions/services/)。 当您设置虚拟机时，请务必使用**HDD**作为磁盘类型时，不**SSD**。

## <a name="frequently-asked-questions"></a>常见问题

本部分包含有关机器学习虚拟机从 Microsoft 的一些常见问题。

### <a name="can-i-install-a-virtual-machine-with-sql-server-2017"></a>可以使用 SQL Server 2017 安装虚拟机？

用于 SQL Server 自 2017 年 1 Enterprise Edition 包含机器学习服务的基于 Windows 的虚拟机将在稍后提供。 寻找这些博客网站上的公告：

+ [Cortana 智能和机器学习](https://blogs.technet.microsoft.com/machinelearning/)
+ [数据平台内部](https://blogs.technet.microsoft.com/dataplatforminsider/)

### <a name="how-do-i-access-data-in-an-azure-storage-account"></a>如何访问 Azure 存储帐户中的数据？

需要使用 Azure 存储帐户中的数据时，有几个选项可用于访问或移动数据：

+ 使用实用工具（如 [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only)）将数据从存储帐户复制到本地文件系统。 

+ 将文件添加到存储帐户上的文件共享，然后在 VM 上以网络驱动器的形式装载文件共享。  有关详细信息，请参阅 [装载 Azure 文件](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/)。 

### <a name="how-do-i-use-data-from-azure-data-lake-storage-adls"></a>如何使用 Azure Data Lake Storage (ADLS) 中的数据？

如果引用相同的方式将 HDFS 文件系统，通过使用 webHDFS 的存储帐户，你可以从使用 RevoScaleR，ADLS 存储读取数据。  有关详细信息，请参阅此文章：[使用 R 来执行 Azure Data Lake 存储上的文件系统操作](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/03/14/using-r-to-perform-filesystem-operations-on-azure-data-lake-store/)。



