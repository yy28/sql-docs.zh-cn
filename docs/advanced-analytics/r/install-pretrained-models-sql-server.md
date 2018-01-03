---
title: "在 SQL Server 上安装预先训练的机器学习模型 |Microsoft 文档"
ms.date: 11/16/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 442f4f434e019da241fcaecb380c967d0f405fd6
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="install-pretrained-machine-learning-models-on-sql-server"></a>安装预先训练的机器学习模型上 SQL Server

本指南介绍了如何将预先训练的模型添加到的 SQL Server 实例已具有 R Services 或机器学习服务安装。

当 Microsoft R Server 或机器学习服务器使用单独的 Windows installer，安装预先训练的模型的选项才可用。 你可以使用此安装程序来获取只需预先训练的模型，或者你可以使用到[升级机器学习组件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)的 SQL Server 2016 或 SQL Server 2017 实例中。

运行安装程序下载预先训练的模型后，有一些附加步骤以使用 SQL Server 配置使用的模型。 本文描述的过程。

有关如何使用 SQL Server 数据，使用预先训练的模型的示例，请参见 SQL Server 机器学习团队的以下博客： 

+ [使用 SQL Server 计算机学习 Services 中的 Python 的观点分析](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/11/01/sentiment-analysis-with-python-in-sql-server-machine-learning-services/)

## <a name="benefits-of-using-pretrained-models"></a>使用预先训练的模型的好处

为帮助的客户需要权限以执行任务，如观点分析或映像特征化，但未安装的资源来获取大型数据集或复杂模型定型，这些预先训练的模型而创建。 使用预先训练的模型，可让你开始文本和图像有效地处理。

当前可用的模型都的观点分析和图像分类深层神经网络 (DNN) 模型。 所有预先训练的模型已使用 Microsoft 的定型[计算网络工具包](https://cntk.ai/Features/Index.html)，或**CNTK**。

每个网络配置的基于以下的引用实现：

+ ResNet-18
+ ResNet 50
+ ResNet 101
+ AlexNet

有关这些模型的详细信息，请参阅[预先训练的机器学习模型观点分析和映像检测](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)

有关深入学习网络以及使用 CNTK 其实现的详细信息，请参阅这些文章：

+ [Microsoft 研究人员算法设置 ImageNet 质询里程碑](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Microsoft 计算网络工具包提供最高效的分布式的深层学习计算性能](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="how-to-install-the-models-on-sql-server"></a>如何在 SQL Server 上安装模型

1. 运行单独的基于 Windows 的安装程序机器学习服务器。 有关下载位置，请参阅：

    + [安装机器学习适用于 Windows 的服务器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
    + [适用于 Windows 安装 R Server 9.1](https://docs.microsoft.com/r-server/install/r-server-install-windows)

2. 要安装的功能的选择取决于您是在获取只的模型，还是在执行使用安装程序的其他更新。
 
    + 如果这是新安装的计算机学习服务器，并且你不想要对 R 或 Python 组件，选择进行其他更改**仅**预先训练的模型选项。 接受所有其他提示，包括许可协议。

    + 若要同时升级的 R 或 Python 组件，选择你想要更新的语言 （R，或 Python，或两者），然后选择预先训练的模型选项。 选择要对其应用这些更改的一个或多个实例。

    + 如果之前安装机器学习服务器并更新的 R 或 Python 组件使用的绑定选项，保留所有以前选择**原样**，并选择预先训练的模型选项。 不要删除任何以前选择的选项;如果这样做，则安装程序中删除组件。

3. 安装完成后，打开 Windows 命令提示符**以管理员身份**，并导航到安装程序启动文件夹中，对于 SQL Server，还包含 Microsoft R 安装。 在 SQL Server 自 2017 年的默认实例，应为文件夹：
    
    `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\SQL2017\x64\`

4. 运行 RSetup.exe 并指示要安装的组件、 版本和包含模型源文件，使用这些示例中所示的命令行自变量的文件夹：

    + 若要使用与模型**R_SERVICES**:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<SQL_DB_instance_folder>\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    例如，若要启用 R，在默认实例的 SQL Server 自 2017 年，预先训练的模型的最新版本的用于将运行此语句：

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    上的命名实例，该命令应为类似如下内容：

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MyInstanceName\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    + 若要使用预先训练的模型与 R Server （独立） 或机器学习 Server （独立版）：

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "~\R_SERVER\library\MicrosoftML\mxLibs\x64"`

    例如，若要启用用于预先训练的模型的最新版本的 R，默认安装的 R Server 的 SQL Server 2016 中将运行此语句：

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir ‘C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\MicrosoftML\mxLibs\"`
    
    + 若要使用与预先训练的模型**PYTHON_SERVICES**:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<SQL_DB_instance_folder>\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    例如，若要启用预先训练的模型的最新版本的用于 Python，在默认实例的 SQL Server 自 2017 年，将运行此语句：

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    上的命名实例，该命令应为类似如下内容：

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MyInstanceName\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    + 若要使用 Python 预先训练模型使用机器学习 Server （独立）：

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<sql_folder>\PYTHON_SERVER\site-packages\microsoftml\mxLibs"`

    例如，假设使用 SQL Server 2017 安装程序的默认安装的计算机学习 Server （独立），运行此语句：

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER\Lib\site-packages\microsoftml\mxLibs"`

5. 版本参数支持以下值：

    + 候选发布版 0: **9.1.0.0**
    + 候选发布版 1: **9.2.0.22**
    + RTM: **9.2.0.100**
    + 累积更新 1: **9.2.0.24**

6. 如果安装成功，应将以下模型添加到您的 R\_服务或 PYTHON\_SERVICES 文件夹：

    - AlexNet\_Updated.model
    - ImageNet1K\_mean.xml
    - pretrained.model
    - ResNet\_101\_Updated.model
    - ResNet\_18\_Updated.model
    - ResNet\_50\_Updated.model


> [!NOTE]
> 
> 如果模型文件的路径太长，从 Python 代码中调用模型文件时可能会出错。 这是因为当前的 Python 实现中的限制。 将在即将发布的服务版本中修复此问题。

## <a name="examples"></a>示例

安装模型后，你可以使用这些模型通过在代码中调用它们。

### <a name="image-featurization-example"></a>图像特征化示例

预先训练的模型的映像支持你所提供的映像的特征。 此特定模型进行定型使用[CNTK](https://docs.microsoft.com/cognitive-toolkit/)。 

若要使用模型，请调用**featurizeImage**转换。

+ [featurizeImage： 机器学习映像特征化转换](https://docs.microsoft.com/r-server/r-reference/microsoftml/featurizeimage)

在此示例中，请参阅代码的第二个块。 在图像加载，调整大小，并通过预先训练的 convolutional DNN 模型的垃圾桶。 DNN 特征化器的输出然后用于训练线性图像分类模型。

必须调整图像大小，以满足经过训练的模型的要求： 用于定型的映像共有 224 x 224 px。 如果你已使用 AlexNet 模型，图像将调整到 227 x 227 px。

```R
 model <- rxFastLinear(
     Label ~ Features,
     data = train,
     mlTransforms = list(
         loadImage(vars = list(Features = "Path")),
         resizeImage(vars = "Features", width = 224, height = 224), 
         extractPixels(vars = "Features"),
         featurizeImage(var = "Features")
         ),
     mlTransformVars = "Path")
```

> [!NOTE]
> 它不能读取或修改预先训练的模型，因为它们压缩的是使用本机格式，以提高性能。

### <a name="text-analysis-example"></a>文本分析示例

请参阅下面的示例演示如何使用文本分类预先训练的文本特征化模型：

[使用文本特征化器的观点分析](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)
