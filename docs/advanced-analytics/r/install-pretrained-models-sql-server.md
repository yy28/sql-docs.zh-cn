---
title: "在 SQL Server 上安装预先训练的机器学习模型 |Microsoft 文档"
ms.date: 03/14/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: fd02766e4020e6f522d50bbd471c5f84c66a998b
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2018
---
# <a name="install-pretrained-machine-learning-models-on-sql-server"></a>安装预先训练的机器学习模型上 SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本指南介绍了如何将预先训练的模型添加到的 SQL Server 实例已具有 R Services 或机器学习服务安装。

为帮助的客户需要权限以执行任务，如观点分析或映像特征化，但未安装的资源来获取大型数据集或复杂模型定型，预先训练的模型包括在 MicrosoftML 而创建。 机器学习 Server 团队创建并定型这些模型来帮助你开始文本和图像有效地处理。 有关详细信息，请参阅[资源](#bkmk_resources)部分中的所述。

有关如何使用 SQL Server 数据，使用预先训练的模型的示例，请参见 SQL Server 机器学习团队的以下博客：

+ [使用 SQL Server 计算机学习 Services 中的 Python 的观点分析](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/11/01/sentiment-analysis-with-python-in-sql-server-machine-learning-services/)

## <a name="install-the-pre-trained-models"></a>安装的预先训练的模型

预先训练的模型可用于以下产品：

+ SQL Server 2016 R Services （数据库）
+ SQL Server 自 2017 年 1 机器学习服务 （数据库）
+ 机器学习服务器（独立）

具体取决于你的 SQL Server 版本，安装进程会稍有不同。 请参阅以下各节，有关每个版本的说明。

> [!NOTE]
> 它不能读取或修改预先训练的模型，因为它们压缩的是使用本机格式，以提高性能。

### <a name="obtain-files-for-an-offline-installation"></a>获取文件进行脱机安装

若要在没有 internet 访问的服务器上安装的预先训练的模型，必须提前下载适当的安装程序并将安装程序复制到服务器上的本地文件夹。 

有关所有 R Server 和机器学习服务器安装程序，请参见此页以进行下载链接：[脱机安装](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)

### <a name="install-pretrained-models-with-sql-server-2016-r-services"></a>使用 SQL Server 2016 R Services 安装预先训练的模型

SQL Server 2016，你可以安装并使用预先训练的 R 模型，仅在第一次升级机器学习调用进程中的组件，**绑定**。 

执行此操作通过 Microsoft R Server 或机器学习 Server、 运行单独的 Windows 安装程序并选择实例或者实例**绑定**。 绑定支持策略与实例关联的实例方法被更改，以允许更加频繁地更新。 

1. 启动单独的基于 Windows 的安装程序或者[R Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server)或[机器学习服务器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)。

2. 选择要升级的实例，然后选择要获取预先训练的模型的选项。

    有关详细信息，请参阅[升级 SQL Server 使用的机器学习组件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

    如果你以前已执行绑定以更新的 R 组件，并只是想要添加预先训练的模型，保留所有以前选择**原样**，并选择预先训练的模型的选项。 
    
    不要删除任何以前选择的选项;如果这样做，则安装程序中删除组件。

3. 我们建议你接受模型位置的默认设置。

4. 接受所有其他提示，包括许可协议。

绑定完成后，使用 R Server 或机器学习服务器中所提供的较新版本替换的 R 版本和与实例关联的库。 

SQL Server 2016，你必须执行一些附加步骤以注册 SQL Server 2016 实例库的模型。 为安装的预先训练的模型的位置每个实例重复这些步骤。

1. 打开 Windows 命令提示符**以管理员身份**。

2. 对于 SQL Server，还包含 Microsoft R 安装程序，导航到安装程序启动文件夹。 在 SQL Server 2016 的默认实例，应为文件夹：
    
    `C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\SQL2017\x64\`

3. 运行`RSetup.exe`并指示要安装的组件、 版本和包含模型源文件，使用此语法的文件夹：

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<SQL_DB_instance_folder>\R_SERVICES\library\MicrosoftML\mxLibs\x64"`中创建已分区表或索引。 

    版本参数支持以下值：

    + 候选发布版 0: **9.1.0.0**
    + 候选发布版 1: **9.2.0.22**
    + RTM: **9.2.0.100**
    + 累积更新 1: **9.2.0.24**
    + 累积更新 4: **9.3.0**

    > [!NOTE]
    > 列出了相应的 SQL Server 版本，以让你的发布更新的时间了解。 如果你不确定的与 SQL Server 安装的版本，打开该实例，R_SERVICES 文件夹并打开 RGui (`~\R_SERVICES\bin\x64`)。 开始屏幕中列出的 Microsoft R Open 版本和机器学习服务器的版本。 

    例如，若要使用预先训练的 R 模型的默认实例与**R_SERVICES**，需要运行以下命令：

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    上的命名实例，该命令应为类似如下内容：

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL13.MyInstanceName\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

4. 如果安装成功，应将以下模型添加到你`R_SERVICES`文件夹：

    + AlexNet\_Updated.model
    + ImageNet1K\_mean.xml
    + pretrained.model
    + ResNet\_101\_Updated.model
    + ResNet\_18\_Updated.model
    + ResNet\_50\_Updated.model

### <a name="install-pretrained-models-on-sql-server-2017"></a>在 SQL Server 2017 上安装预先训练的模型

如果你已经安装了 SQL Server 自 2017 年，你可以两种方式获得预先训练的模型：

+ 通过使用绑定，升级的 Python 和 R 组件和在同一时间安装的预先训练的模型
+ 安装仅预先训练的模型

以下说明介绍了如何升级的机器学习组件，并在同一时间获取预先训练的模型。

1. 运行基于 Windows 的计算机学习服务器安装程序。 你可以从在此页上的链接下载安装程序：[安装机器学习用于 Windows 的服务器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)。

2. 如果你将安装到没有 internet 访问的服务器的模型，请确保也从此页中下载的安装程序预先训练的模型：[机器学习服务器的脱机安装](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)。

3. 运行安装程序。

4. 若要同时升级的 R 或 Python 组件，选择你想要更新的语言 （R，或 Python，或两者）。

    如果之前安装机器学习服务器并更新的 R 或 Python 组件使用的绑定选项，保留所有以前选择**原样**，并选择预先训练的模型选项。 不要删除任何以前选择的选项;如果这样做，则安装程序中删除组件。

5. 接受所有其他提示，包括许可协议。

使用 SQL Server 自 2017 年，不不需要任何其他配置。

> [!NOTE]
> 
> 对于 Python 模型，只有在从 Python 代码中调用模型文件时可能会出错。 这是路径的因为在当前的 Python 实现中，限制该限制的模型文件长度。 此问题已修复，并将在即将发布的服务版本中可用。

### <a name="installing-pretrained-models-with-r-server-standalone"></a>使用 R Server （独立） 安装预先训练的模型

如果你安装早期版本的 R Server （独立） 使用 SQL Server 2016 安装程序，可以添加预先训练的模型使用通过 R 服务器使用较新的基于 Windows 的安装程序升级的能力。 

预先训练的模型首次推出作为可选项随[Microsoft R Server 9.1](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/introducing-microsoft-r-server-9-1-release/)，但每个版本中添加了升级。 我们建议获取最新版本，但此处也列出以前的发行版[R Server 释放](https://docs.microsoft.com/machine-learning-server/install/r-server-install)

下面的说明介绍如何升级的 R 组件，并在同一时间将添加预先训练的模型。

1. 启动单独的基于 Windows 的安装程序或者[R Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server)或[机器学习服务器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)。

2. 选择你想要更新，然后选择的语言**Pre-trained 模型**选项。

    > [!TIP]
    > 如果你以前运行安装程序来更新 R Server （独立），并只是想要添加预先训练的模型，保留所有以前选择**原样**，然后选择刚预**-定型模型**选项. **不这样做**取消选择任何以前选择的选项; 如果这样做，则安装程序中删除组件。

    我们建议你接受模型位置的默认设置。

3. 单击 **“继续”**。 

4. 接受所有其他提示，包括许可协议。

安装完成后，你必须执行一些附加步骤以注册预先训练的模型。

1. 打开 Windows 命令提示符**以管理员身份**。

2. R server （独立），还包含 Microsoft R 安装程序，导航到安装程序启动文件夹。 

3. 运行`RSetup.exe`并指示要安装的组件、 版本和包含模型源文件，使用此语法的文件夹：

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "~\R_SERVER\library\MicrosoftML\mxLibs\x64"`

    版本参数支持以下值：

    + 候选发布版 0: **9.1.0.0**
    + 候选发布版 1: **9.2.0.22**
    + RTM: **9.2.0.100**
    + 累积更新 1: **9.2.0.24**
    + 累积更新 4: **9.3.0**

    例如，若要启用用于预先训练的模型的最新版本的 R，在默认安装 R Server （独立），将运行此语句：

    `RSetup.exe /install /component MLM /version 9.3.0 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\MicrosoftML\mxLibs\"`

### <a name="installing-pretrained-models-with-machine-learning-server-standalone"></a>使用机器学习 Server （独立） 安装预先训练的模型

如果你安装使用 SQL Server 2017 安装程序的机器学习服务器，可以通过运行基于 Windows 的安装程序添加预先训练的模型。 可以选择此选项以升级 R 或 Python 组件中，并同时添加预先训练的模型。 

安装完成后，不不需要任何其他配置。

## <a name="bkmk_resources"></a> 研究和资源

当前可用的模型都的观点分析和图像分类深层神经网络 (DNN) 模型。 所有预先训练的模型已使用 Microsoft 的定型[计算网络工具包](https://cntk.ai/Features/Index.html)，或**CNTK**。

每个网络配置的基于以下的引用实现：

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

有关在学习模型，以及它们 ere 实现和定型使用 CNTK 这些深层中使用的算法的详细信息，请参阅这些文章：

+ [Microsoft 研究人员算法设置 ImageNet 质询里程碑](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Microsoft 计算网络工具包提供最高效的分布式的深层学习计算性能](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

### <a name="how-to-use-pre-trained-models-for-text-analysis"></a>如何使用预先训练的模型进行文本分析

请参阅下面的示例演示如何使用文本分类预先训练的文本特征化模型：

[使用文本特征化器的观点分析](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

### <a name="how-to-use-pretrained-models-for-image-detection"></a>如何将预先训练的模型用于映像检测

预先训练的模型的映像支持你提供的映像的特征。 若要使用模型，请调用**featurizeImage**转换。 在图像加载，调整大小，并通过经过训练的模型的垃圾桶。 DNN 特征化器的输出然后用于训练线性图像分类模型。

若要使用此模型，所有映像必须都调整以满足经过训练的模型的要求。 例如，如果您使用 AlexNet 模型，该图像应调整到 227 x 227 px。

有关详细信息，请参阅[观点分析和映像检测预先训练的模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)
