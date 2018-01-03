---
title: "设置用于在 Azure 上的机器学习的虚拟机 |Microsoft 文档"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c8826df7-aa67-4768-baa9-bdc875c4a766
caps.latest.revision: "12"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 4887d79f60a8fd418fd4a5543bbac9dec0af3ebc
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="provision-a-virtual-machine-for-machine-learning-on-azure"></a>设置用于在 Azure 上的机器学习的虚拟机

在 Azure 上的虚拟机是一个方便的选项，用于快速配置用于机器学习解决方案的完整的服务器环境。

本文列出了包含与机器学习，，以及一些相关的虚拟机的 SQL Server 的虚拟机映像。

本文还提供了修改或升级现有的虚拟机中 SQL Server 实例有关的常见问题的答案。

+ [当前虚拟机的列表](#bkmk_list)

## <a name="provision-a-virtual-machine-with-sql-server-and-machine-learning"></a>设置与 SQL Server 的虚拟机和机器学习

如果你不熟悉如何使用 Azure Vm，我们建议你看到这些文章以获取有关使用门户和配置虚拟机的详细信息。

+ [虚拟机 - 入门](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)
+ [如何开始使用 Windows 虚拟机](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/)

请务必使用 Azure 门户或 Azure 应用商店的新版本。 在浏览经典门户上的 Azure 库时，某些图像不可用。

**创建虚拟机**

1. 打开 Azure 门户： [portal.azure.com](https:portal.azure.com)。

2. 单击**虚拟机**，或单击**新建**。

3. 单击 **“添加”**。

4. 在页面顶部的搜索框中，键入"机器学习 Server"或"SQL Server"，以查看相关虚拟机的列表。

5. 查看要求，并单击**创建**吧。

6. 虚拟机已创建并运行后，单击**连接**按钮以打开连接并登录到新计算机。

5. 连接后，你可以安装其他 R 或 Python 软件包，或配置你的首选的开发工具。

### <a name="connect-to-the-virtual-machine"></a>连接到虚拟机

客户端连接到虚拟机上运行的 SQL Server 的方式有所不同具体取决于客户端和网络配置的位置。

有关详细信息，请参阅[连接到 Azure 上的 SQL Server 虚拟机](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-connect)。

## <a name="frequently-asked-questions"></a>常见问题

本部分包含有关机器学习虚拟机从 Microsoft 的一些常见问题。

### <a name="can-i-install-a-virtual-machine-with-sql-server-2017"></a>可以使用 SQL Server 2017 安装虚拟机？

基于 Windows 的虚拟机的 SQL Server 自 2017 年 1 Enterprise Edition 包含机器学习服务可从自 2017 年 11 月。 

有关新数据科学虚拟机的公告，观看这些博客站点：

+ [Cortana 智能和机器学习](https://blogs.technet.microsoft.com/machinelearning/)
+ [数据平台内部](https://blogs.technet.microsoft.com/dataplatforminsider/)

### <a name="adding-sql-server-to-an-existing-virtual-machine"></a>将 SQL Server 添加到现有的虚拟机

除了创建虚拟机使用已包含 SQL Server 机器学习，你可以在现有虚拟机上安装 SQL Server，启用机器学习功能的映像。 我们建议使用企业或开发人员版，以避免资源约束。 安装也要求你使用你自己的许可证密钥。

运行安装程序时，请务必选择机器学习功能和至少一种语言 （R 或 Python）。 执行一些其他步骤都需要启用机器学习服务与 SQL Server 通信，以使虚拟机上的网络。

有关详细信息，请参阅[安装 Azure 虚拟机上 SQL Server R Services](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)。

### <a name="using-machine-learning-in-azure-sql-database"></a>使用 Azure SQL 数据库中的机器学习

中的开始在 2017 年，Azure SQL 数据库支持使用 R 来训练模型并将其用于预测。 

R Services 数据库中可作为预览功能仅，并具有与 SQL Server 的本地版本相比某些限制。 有关详细信息，请参阅[Azure SQL DB](../r/using-r-in-azure-sql-database.md)。

### <a name="can-i-upgrade-the-sql-server-version-on-a-virtual-machine"></a>可以升级虚拟机上的 SQL Server 版本？

尽管 SQL Server 2016 映像支持 R，如果你想要使用 Python，你可以升级到 SQL Server 2017，也会升级其他机器学习组件。

若要更新的安装的 SQL Server 版本，打开 SQL Server 安装中心上虚拟机，然后选择**升级**选项。 具体取决于哪个虚拟机所创建的许可证可能需要。

有关详细信息，请参阅[使用安装向导升级 SQL Server](https://docs.microsoft.com/sql/database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup)。

### <a name="can-i-upgrade-just-the-machine-learning-components"></a>可以升级只是机器学习组件？

新升级的 RevoScaleR、 MicrosoftML 或 revoscalepy 发布，你可以升级机器学习使用称为的过程使用 SQL Server，组件_绑定_。 这不会更改你的 SQL Server 版本，但它会更改实例的支持策略。

有关详细信息，请参阅[使用 SqlBindR 升级 SQL Server 上的机器学习组件](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

### <a name="how-do-i-access-data-in-an-azure-storage-account"></a>如何访问 Azure 存储帐户中的数据？

需要使用 Azure 存储帐户中的数据时，有几个选项可用于访问或移动数据：

+ 使用实用工具（如 [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only)）将数据从存储帐户复制到本地文件系统。 

+ 将文件添加到存储帐户上的文件共享，然后在 VM 上以网络驱动器的形式装载文件共享。 有关详细信息，请参阅 [装载 Azure 文件](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/)。 

### <a name="how-do-i-use-data-from-azure-data-lake-storage-adls"></a>如何使用 Azure Data Lake Storage (ADLS) 中的数据？

你可以从使用 RevoScaleR，通过使用 webHDFS 引用相同的方式将 HDFS 文件系统的存储帐户的 ADLS 存储读取数据。 有关详细信息，请参阅此文章：[使用 R 来执行 Azure Data Lake 存储上的文件系统操作](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/03/14/using-r-to-perform-filesystem-operations-on-azure-data-lake-store/)。

### <a name="i-cant-find-the-rre-virtual-machine"></a>找不到 RRE 虚拟机

在以前提供的"RRE 为 Windows 虚拟机"的"机器学习用于 Windows 的服务器"映像替换为 Azure 应用商店。

机器学习 Server 映像也已可用于 Linux CentOS 版本 7.2、 Linux RedHat 版本 7.2 和 Ubuntu 版本 16.04。

有关详细信息，请参阅[云中的机器学习服务器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-in-the-cloud)

### <a name="configuring-machine-learning-server-or-r-server-to-support-web-services"></a>配置机器学习服务器或 R Server，以支持 web 服务

如果你使用包含机器学习服务器的虚拟机，其他配置可能需要使用 web 服务部署，远程执行，或使用为你的组织中的部署服务器的虚拟机。

有关说明，请参阅[配置机器学习服务器以具有可操作性分析](https://docs.microsoft.com/machine-learning-server/operationalize/configure-machine-learning-server-one-box)。

如果你只是想要使用如 RevoScaleR 或 MicrosoftML 的包，则不需要其他配置。

## <a name="bkmk_list"></a>虚拟机的列表

目前，以下虚拟机是可用于机器学习与 SQL Server:

|“属性”| 注释|
|----|----|----|
| **SQL Server 2016**| ***  |
|在 Windows 上的 SQL Server 2016 SP1 Enterprise|集成的高级分析的 R Services。|
|Windows Server 上的 BYOL SQL Server 2016 SP1 Enterprise |集成的高级分析的 R Services。 |
|Windows Server 2016 上的可用许可证： SQL Server 2016 SP1 开发人员 |集成的高级分析的 R Services。 |
| 数据科学虚拟机的 Windows 2012|包含用于数据科学，。 包括 Microsoft R Server Developer Edition、 SQL Server 2016 开发人员版、 Anaconda Python 分发，Julia 专业开发人员版和 Jupyter 笔记本的常用工具| 
| 数据科学虚拟机-Windows 2016|包含 SQL Server 2016 Developer Edition，具有对数据库中 R 分析的支持。|
|**SQL Server 2017**| ***   |
|SQL Server 自 2017 年企业 Windows Server 2016| 具有 Python 和 R 语言支持的机器学习服务。|
|BYOL SQL Server 自 2017 年企业 Windows Server 2016|具有 Python 和 R 语言支持的机器学习服务。|
| Windows Server 上可用的 SQL Server 许可证： SQL Server 自 2017 年 Developer|具有 Python 和 R 语言支持的机器学习服务。|
| **其他**| *** |
| 机器学习服务器唯一的 SQL Server 自 2017 年 Enterprise|类似于 SQL Server 2016 Enterprise 映像，但包含的机器学习服务器的独立版本，但核心 ScaleR 和操作化功能优化适用于 Windows 环境。|
| 适用于 Windows 的机器学习服务器|机器学习服务器的独立版本包含针对 Windows 环境而优化的操作化功能。|
|数据科学虚拟机 |Linux 版本包括 R Server。 包括 SQL Server 自 2017 年的 Linux 虚拟机无法在 SQL Server 中运行 R 或 Python 代码。 但是，你可以执行使用 T-SQL 的预测函数的训练模型评分。 有关详细信息，请参阅[SQl Server 中的本机评分](../sql-native-scoring.md)。|
