---
title: "在 SQL Server 上安装预先训练的机器学习模型 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: b52fcc1e4ac77df2968a4ea6cbd6e546ff1b74ac
ms.contentlocale: zh-cn
ms.lasthandoff: 09/19/2017

---
# <a name="install-pretrained-machine-learning-models-on-sql-server"></a>安装预先训练的机器学习模型上 SQL Server

本主题介绍如何将预先训练的模型添加到的 SQL Server 实例已具有 R Services 或机器学习服务安装。

预先训练的模型与更新提供给 Microsoft R Server （或 Microsoft 机器学习 Server 的更新）。 有关如何升级你的实例和获取 Microsoft R 最新版本的信息，请参阅[升级 R Services 的实例中的 R 组件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

仅运行单独的基于 Windows 的安装程序 R Server 可以安装这些模型。
但是，有一些附加步骤以在 SQL Server 上安装模型时使用。 本主题描述的过程。

## <a name="benefits-of-using-pretrained-models"></a>使用预先训练的模型的好处

进行了预先训练的模型可用于支持需要执行任务，如观点分析或图像特征化，但没有足够的资源，以获取大型数据集或复杂模型定型的客户。 使用预先训练的模型，可让你开始文本和图像最有效地处理。

当前可用的模型都的观点分析和图像分类深层神经网络 (DNN) 模型。 所有四个预先训练的模型已接受有关 CNTK 的培训。 每个网络配置的基于以下的引用实现：

+ ResNet-18
+ ResNet 50
+ ResNet 101
+ AlexNet

有关深入残留网络以及使用 CNTK 其实现的详细信息，请参阅这些文章：

+ [Microsoft 研究人员算法设置 ImageNet 质询里程碑](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Microsoft 计算网络工具包提供最高效的分布式的深层学习计算性能](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="how-to-install-the-models-on-sql-server"></a>如何在 SQL Server 上安装模型

   > [!NOTE]
   > 
   > 如果要安装 Microsoft R Server 或升级你的 SQL Server 实例使用单独的基于 Windows 的安装，安装程序提供了预先训练的模型。 请参阅[适用于 Windows 的安装 R Server](https://docs.microsoft.com/en-us/r-server/install/r-server-install-windows)。
   > 
   > 与 Microsoft R Server 一起使用的模型可能需要一些附加步骤。 有关详细信息，请参阅[如何安装和部署预先训练机器学习模型与 MicrosoftML](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models)

1. 安装 SQL Server; 时，默认情况下未安装的预先训练的模型SQL Server 安装程序已完成后运行命令行安装实用程序，必须将它们添加。

2. 打开提升的命令提示符，并导航到安装程序启动文件夹中，对于 SQL Server，还包含 Microsoft R 安装。

    在 SQL Server 自 2017 年 1 RC 1 的默认实例，这将是：
    
    `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\SQL2017RC1\x64\`

3. 指定要安装的组件和预先训练的模型应在将添加位置，通过使用以下参数的文件夹：

  + 若要使用与模型**R_SERVICES**

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir <SQL_DB_instance_folder>\R_SERVICES`

    例如，若要启用使用预先训练的模型使用的 SQL Server 自 2017 年的默认实例中的 R，将运行此语句：

    `RSetup.exe /install /component MLM /version 9.2.0.22 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES"`

  + 若要使用与模型**PYTHON_SERVICES**

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir <SQL_DB_instance_folder>\PYTHON_SERVICES`

    例如，若要启用使用预先训练的模型使用 Python，对于默认实例的 SQL Server 自 2017 年，将运行此语句：

    `RSetup.exe /install /component MLM /version 9.2.0.22 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES"`

4. 对于版本参数中，支持以下值：

    + 候选发布版 0: **9.1.0.0**
    + 候选发布版 1: **9.2.0.22**
    + （不释放） 的最终版本数： **9.2.0.100**

5. 如果安装成功，应将以下模型添加到您的 R\_服务或 PYTHON\_SERVICES 文件夹：

    - AlexNet_Updated.model
    - ImageNet1K_mean.xml
    - pretrained.model
    - ResNet_101_Updated.model
    - ResNet_18_Updated.model
    - ResNet_50_Updated.model

## <a name="examples"></a>示例

安装模型后，你可以通过调用它们 R 代码中使用这些模型。

### <a name="image-featurization-example"></a>图像特征化示例

预先训练的模型的映像支持你所提供的映像的特征。 若要使用模型，请调用**featurizeImage**转换。

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
> 
> 不能读取或修改预先训练的模型本身。 此特定模型基于[CNTK](https://docs.microsoft.com/cognitive-toolkit/)模型，但已使用本机格式，出于性能原因被压缩。

### <a name="text-analysis-example"></a>文本分析示例

此示例演示预先训练的模型用于分类：

[使用文本特征化器的观点分析](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

