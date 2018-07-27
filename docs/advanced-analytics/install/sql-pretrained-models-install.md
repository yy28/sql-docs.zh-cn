---
title: SQL Server 上安装预先定型的机器学习模型 |Microsoft Docs
description: 将预先训练的情绪分析和图像特征化的模型添加到 SQL Server 2017 机器学习服务 （R 或 Python） 或 SQL Server 2016 R Services。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/18/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b2dfee04a7c0c9c39b7969551a85a49d441f30e5
ms.sourcegitcommit: 84cc5ed00833279da3adbde9cb6133a4e788ed3f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2018
ms.locfileid: "39216828"
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>安装预先定型的机器学习模型的 SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

此文章介绍了如何使用 Powershell 来添加免费预先训练的机器学习模型*情绪分析*并*图像特征化*到具有 R 或 Python 的 SQL Server 数据库引擎实例集成。 预先训练的模型构建由 Microsoft 和随时可用，添加到数据库引擎实例作为安装后任务。 有关这些模型的详细信息，请参阅[资源](#bkmk_resources)本文的部分。

安装后，预先训练的模型被视为 power MicrosoftML (R) 和 microsoftml (Python) 库中的特定函数的实现细节。 您不应 （和无法） 查看、 自定义，或重新训练模型，也可以在将其视为独立的资源中的自定义代码或配对的其他函数。 

若要使用预先训练的模型，请调用以下表中列出的函数。

| R 函数 (MicrosoftML) | Python 函数 (microsoftml) | 用法 |
|--------------------------|-------------------------------|-------|
| [getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | [get_sentiment](https://docs.microsoft.com//machine-learning-server/python-reference/microsoftml/get-sentiment) | 生成对文本输入正数负数情绪分数。 [了解详细信息](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/11/01/sentiment-analysis-with-python-in-sql-server-machine-learning-services/)。|
| [featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | [featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | 从图像文件输入中提取文本信息。 [了解详细信息](https://blogs.msdn.microsoft.com/mlserver/2017/04/12/image-featurization-with-a-pre-trained-deep-neural-network-model/)。 |

## <a name="prerequisites"></a>必要條件

机器学习算法是计算密集型操作。 我们建议使用 16 GB RAM 对于低到中等工作负荷，包括使用的所有示例数据的教程演练完成。

必须具有计算机和 SQL Server 上的管理员权限才能添加预先训练的模型。

必须启用外部脚本，并且必须运行 SQL Server LaunchPad 服务。 安装说明提供有关启用和验证这些功能的步骤。 

[MicrosoftML R 包](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)或[microsoftml Python 包](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)包含预先训练的模型。

+ [SQL Server 2017 机器学习服务](sql-machine-learning-services-windows-install.md)包括机器学习库，这两个语言版本，因此您采取任何进一步的操作与满足此先决条件。 由于存在这些库时，可以使用本文中所述的 PowerShell 脚本将预先训练的模型添加到这些库。

+ [SQL Server 2016 R Services](sql-r-services-windows-install.md)，即 R，不包括[MicrosoftML 包](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)现成的。 若要添加 MicrosoftML，必须执行[组件升级](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。 组件升级的一个优点是，您可以同时添加预先训练的模型，从而运行不必要的 PowerShell 脚本。 但是，如果你已升级，但缺少添加第一次的预先训练的模型，您可以运行 PowerShell 脚本，如这篇文章中所述。 它适用于这两个版本的 SQL Server。 执行之前，请确认 MicrosoftML 库位于 C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\R_SERVICES\library。


<a name="file-location"></a>

## <a name="check-whether-pre-trained-models-are-installed"></a>检查是否安装预先训练的模型

R 和 Python 模型的安装路径如下所示：

+ 为: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64`

+ 对于 Python: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs `

下面列出了模型文件的名称：

+ AlexNet\_Updated.model
+ ImageNet1K\_mean.xml
+ pretrained.model
+ ResNet\_101\_Updated.model
+ ResNet\_18\_Updated.model
+ ResNet\_50\_Updated.model

如果已安装模型，跳到[验证步骤](#verify)确认是否可用。

## <a name="download-the-installation-script"></a>下载安装脚本

单击[ https://aka.ms/mlm4sql ](https://aka.ms/mlm4sql)若要下载该文件**安装 MLModels.ps1**。

## <a name="execute-with-elevated-privileges"></a>使用提升的权限执行

1. 启动 PowerShell。 在任务栏中，右键单击 PowerShell 程序图标并选择**以管理员身份运行**。
2. 输入安装脚本文件的完全限定路径，包括实例名称。 假设下载文件夹和默认实例，该命令可能如下所示：

   ```powershell
   PS C:\WINDOWS\system32> C:\Users\<user-name>\Downloads\Install-MLModels.ps1 MSSQLSERVER
   ```

**输出**

连接到 internet 的 SQL Server 2017 机器学习默认实例上使用 R 和 Python，您应看到类似于以下的消息。

   ```powershell
   MSSQL14.MSSQLSERVER
        Verifying R models [9.2.0.24]
        Downloading R models [C:\Users\<user-name>\AppData\Local\Temp]
        Installing R models [C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\]
        Verifying Python models [9.2.0.24]
        Installing Python models [C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\]
   PS C:\WINDOWS\system32>
   ```

<a name="verify"> </a>

## <a name="verify-installation"></a>验证安装

首先，检查新文件中[mxlibs 文件夹](#file-location)。 接下来，运行演示代码以确认模型是安装并正常工作。 

### <a name="r-verification-steps"></a>R 验证步骤

1. 启动**RGUI。EXE**在 C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\R_SERVICES\bin\x64。

2. 在下面的 R 脚本的命令提示符处粘贴。

    ```r
    # Create the data
    CustomerReviews <- data.frame(Review = c(
    "I really did not like the taste of it",
    "It was surprisingly quite good!",
    "I will never ever ever go to that place again!!"),
    stringsAsFactors = FALSE)

    # Get the sentiment scores
    sentimentScores <- rxFeaturize(data = CustomerReviews, 
                                    mlTransforms = getSentiment(vars = list(SentimentScore = "Review")))

    # Let's translate the score to something more meaningful
    sentimentScores$PredictedRating <- ifelse(sentimentScores$SentimentScore > 0.6, 
                                            "AWESOMENESS", "BLAH")

    # Let's look at the results
    sentimentScores
    ```

3. 按 Enter 以查看情绪分数。 输出应如下所示：

    ```
    > sentimentScores
                                            Review SentimentScore
    1           I really did not like the taste of it      0.4617899
    2                 It was surprisingly quite good!      0.9601924
    3 I will never ever ever go to that place again!!      0.3103435
    PredictedRating
    1            BLAH
    2     AWESOMENESS
    3            BLAH
    ```

### <a name="python-verification-steps"></a>Python 验证步骤

1. 启动**Python.exe**在 C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES。

2. 在下面的 Python 脚本的命令提示符处粘贴

    ```python
    import numpy
    import pandas
    from microsoftml import rx_logistic_regression, rx_featurize, rx_predict, get_sentiment

    # Create the data
    customer_reviews = pandas.DataFrame(data=dict(review=[
                "I really did not like the taste of it",
                "It was surprisingly quite good!",
                "I will never ever ever go to that place again!!"]))
                
    # Get the sentiment scores
    sentiment_scores = rx_featurize(
        data=customer_reviews,
        ml_transforms=[get_sentiment(cols=dict(scores="review"))])
        
    # Let's translate the score to something more meaningful
    sentiment_scores["eval"] = sentiment_scores.scores.apply(
                lambda score: "AWESOMENESS" if score > 0.6 else "BLAH")
    print(sentiment_scores)
    ```

3. 按 Enter 可以打印评分。 输出应如下所示：

    ```
    >>> print(sentiment_scores)
                                                review    scores         eval
    0            I really did not like the taste of it  0.461790         BLAH
    1                  It was surprisingly quite good!  0.960192  AWESOMENESS
    2  I will never ever ever go to that place again!!  0.310344         BLAH
    >>>
    ```

> [!NOTE]
> 如果演示脚本失败，请首先检查文件位置。 在系统上有多个 SQL Server 实例或为实例运行的并行与独立版本，可能会安装脚本错误读取环境并将文件放在错误的位置。 通常情况下，将文件手动复制到正确 mxlib 文件夹可以解决问题。

## <a name="examples-using-pre-trained-models"></a>使用预先训练的模型示例

以下链接包括调用预先训练的模型的演练和示例代码。

+ [使用 SQL Server 机器学习服务中的 Python 进行情绪分析](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/11/01/sentiment-analysis-with-python-in-sql-server-machine-learning-services/)

+ [使用预先训练的深度神经网络模型的图像特征化](https://blogs.msdn.microsoft.com/mlserver/2017/04/12/image-featurization-with-a-pre-trained-deep-neural-network-model/)

  对于映像预先训练的模型支持您提供的映像的特征化。 若要使用的模型，请调用**featurizeImage**转换。 加载图像时，调整大小，并具有以下特征的训练模型。 然后使用 DNN 特征化器的输出是训练图像分类的线性模型。 若要使用此模型中，所有映像必须调整都大小以满足已训练模型的要求。 例如，如果您使用 AlexNet 模型，映像应调整为 227 x 227 像素。

+ [代码示例： 使用文本特征化器进行情绪分析](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

<a name="bkmk_resources"></a> 

## <a name="research-and-resources"></a>研究和资源

当前可用的模型都深度神经网络 (DNN) 的情绪分析和图像分类模型。 所有预先训练的模型所使用的是 Microsoft 的训练[计算网络工具包](https://cntk.ai/Features/Index.html)，或**CNTK**。

以下参考实现的基础的每个网络配置：

+ ResNet 18
+ ResNet-50
+ ResNet-101
+ AlexNet

这些深度学习模型和如何实现中使用的算法的详细信息，并使用 CNTK 训练，请参阅以下文章：

+ [Microsoft 研究人员算法会设置 ImageNet 质询里程碑](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Microsoft 计算网络工具包提供了最高效的分布式的深度学习的计算性能](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="see-also"></a>另请参阅

+ [SQL Server 2016 R 服务](sql-r-services-windows-install.md)
+ [SQL Server 2017 机器学习服务](sql-machine-learning-services-windows-install.md)
+ [升级 SQL Server 实例中的 R 和 Python 组件](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)
+ [适用于 R 的 MicrosoftML 包](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ [用于 Python 的 microsoftml 包](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)
