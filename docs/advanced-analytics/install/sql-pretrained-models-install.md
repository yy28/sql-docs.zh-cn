---
title: 安装预先训练的机器学习模型
description: 添加预先训练的模型, 以供情绪分析和 image 特征化 SQL Server 2017 机器学习服务 (R 或 Python) 或 SQL Server 2016 R Services。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: f89e638b6b9486b17974a04af6076e6c7154fa88
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470350"
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>在 SQL Server 上安装预先训练的机器学习模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍如何使用 Powershell 将免费预先*训练的机器*学习模型*添加到具有*R 或 Python 集成的 SQL Server 实例中。 预先训练的模型由 Microsoft 生成并随时可用, 作为安装后任务添加到实例。 有关这些模型的更多信息，请参阅本文的[资源](#bkmk_resources)部分。

安装后，预先训练的模型将被视为 MicrosoftML (R) 和 microsoftml (Python) 库中支持特定功能的实现细节。 不应（也不能） 查看、自定义或重新训练模型，也不能将其视为自定义代码中的独立资源或视为配对的其他函数。 

若要使用预先训练模型, 请调用下表中列出的函数。

| R 函数 (MicrosoftML) | Python 函数 (microsoftml) | 用法 |
|--------------------------|-------------------------------|-------|
| [getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | [get_sentiment](https://docs.microsoft.com//machine-learning-server/python-reference/microsoftml/get-sentiment) | 在文本输入上生成情绪分数。 |
| [featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | [featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | 从图像文件输入中提取文本信息。 |

## <a name="prerequisites"></a>系统必备

机器学习算法是计算密集型的。 对于低到中等工作符合，建议使用 16 GB RAM，包括使用所有示例数据完成教程演练。

您必须拥有计算机的管理员权限, 并 SQL Server 添加预先训练的模型。

必须启用外部脚本, 并且必须运行启动板服务 SQL Server。 安装说明提供了用于启用和验证这些功能的步骤。 

[MicrosoftML R package](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)或[MicrosoftML Python package](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)包含预先训练的模型。

+ [SQL Server 2017 机器学习服务](sql-machine-learning-services-windows-install.md)包括机器学习库的两种语言版本，因此无需采取进一步操作即可满足此先决条件。 由于存在库，因此可以使用本文介绍的 PowerShell 脚本将预先训练的模型添加到这些库中。

+ [SQL Server 2016 R Services](sql-r-services-windows-install.md)（仅限R）不包含随时可用的 [MicrosoftML 包](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)。 要添加 MicrosoftML，必须执行[组件升级](../install/upgrade-r-and-python.md)。 组件升级的一个优点是你可以同时添加预先训练的模型，这使得无需运行 PowerShell 脚本。 但是，如果已经升级但是第一次升级时未添加预先训练的模型，则可以按照本文所述运行 PowerShell 脚本。 它适用于两个版本的 SQL Server。 在此之前，请确认 MicrosoftML 库在 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library 中。


<a name="file-location"></a>

## <a name="check-whether-pre-trained-models-are-installed"></a>检查是否安装了预先训练的模型

R 和 Python 模型的安装路径如下所示:

+ 对于 R:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64`

+ 对于 Python:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs`

下面列出了模型文件名:

+ AlexNet\_Updated.model
+ ImageNet1K\_mean.xml
+ pretrained.model
+ ResNet\_101\_已更新。模型
+ ResNet\_18\_已更新。模型
+ ResNet\_50\_Updated.model

如果已安装这些模型, 请跳到[验证步骤](#verify)以确认可用性。

## <a name="download-the-installation-script"></a>下载安装脚本

单击[https://aka.ms/mlm4sql](https://aka.ms/mlm4sql)下载**Install-MLModels**文件。

## <a name="execute-with-elevated-privileges"></a>以提升的权限执行

1. 启动 PowerShell。 在任务栏上, 右键单击 PowerShell 程序图标, 然后选择 "以**管理员身份运行**"。
2. 输入安装脚本文件的完全限定路径, 并包括实例名称。 假设下载文件夹和默认实例, 该命令可能如下所示:

   ```powershell
   PS C:\WINDOWS\system32> C:\Users\<user-name>\Downloads\Install-MLModels.ps1 MSSQLSERVER
   ```

**输出**

在连接 internet 的 SQL Server 2017 机器学习使用 R 和 Python 的默认实例上, 应会看到类似于以下内容的消息。

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

首先, 检查[mxlibs 文件夹](#file-location)中的新文件。 接下来, 运行演示代码以确认模型已安装且正常工作。 

### <a name="r-verification-steps"></a>R 验证步骤

1. 启动**rgui.exe。EXE**在 C:\Program FILES\MICROSOFT SQL Server\MSSQL14。MSSQLSERVER\R_SERVICES\bin\x64.

2. 在命令提示符下粘贴以下 R 脚本。

    ```R
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

3. 按 Enter 查看情绪分数。 输出应如下所示:

    ```R
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

1. 在 C:\Program Files\Microsoft SQL Server\MSSQL14. 启动**Python。** MSSQLSERVER\PYTHON_SERVICES.

2. 在命令提示符下粘贴以下 Python 脚本

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

3. 按 Enter 打印分数。 输出应如下所示:

    ```python
    >>> print(sentiment_scores)
                                                review    scores         eval
    0            I really did not like the taste of it  0.461790         BLAH
    1                  It was surprisingly quite good!  0.960192  AWESOMENESS
    2  I will never ever ever go to that place again!!  0.310344         BLAH
    >>>
    ```

> [!NOTE]
> 如果演示脚本失败, 请首先检查文件位置。 在具有多个 SQL Server 实例的系统上, 或对于与独立版本并行运行的实例, 安装脚本可能会错误地读取环境, 并将文件放在错误的位置。 通常, 手动将文件复制到正确的 mxlib 文件夹会解决此问题。

## <a name="examples-using-pre-trained-models"></a>使用预先训练的模型的示例

下面的链接包含调用预先训练模型的示例代码。

+ [代码示例:使用文本特征化器情绪分析](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

<a name="bkmk_resources"></a> 

## <a name="research-and-resources"></a>研究和资源

目前可用的模型是用于情绪分析和图像分类的深层神经网络 (DNN) 模型。 所有预先训练的模型都使用 Microsoft[计算网络工具包](https://cntk.ai/Features/Index.html)或**CNTK**进行训练。

每个网络的配置都基于以下参考实现:

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

有关这些深度学习模型中使用的算法的详细信息, 以及如何使用 CNTK 实现和定型它们的详细信息, 请参阅以下文章:

+ [Microsoft 研究员的算法设置 ImageNet 质询里程碑](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Microsoft 计算网络工具包提供最有效的分布式深度学习计算性能](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="see-also"></a>另请参阅

+ [SQL Server 2016 R Services](sql-r-services-windows-install.md)
+ [SQL Server 2017 机器学习服务](sql-machine-learning-services-windows-install.md)
+ [升级 SQL Server 实例中的 R 和 Python 组件](../install/upgrade-r-and-python.md)
+ [适用于 R 的 MicrosoftML 包](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ [用于 Python 的 microsoftml 包](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)
