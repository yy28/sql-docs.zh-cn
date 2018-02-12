---
title: RevoScaleR | Microsoft Docs
ms.custom: 
ms.date: 11/29/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 8f5df8a224b67be06e5459fc8a65277ddc05f4f6
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2018
---
# <a name="revoscaler"></a>RevoScaleR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

RevoScaleR 是由 Microsoft，支持在规模较大的数据科学提供的机器学习函数的包。

+ 函数支持数据导入、 数据转换、 汇总、 可视化和分析。

+ _大规模_意味着操作可以针对大型数据集，以并行执行并在分布式文件系统。 算法可以在不适合在内存中，通过使用分块，以及通过组装结果完成操作后的数据集上进行操作。

+ RevoScaleR 基础上开放源代码 R 函数提供了许多改进。 没有对应于许多最常用的基础 R 函数的 RevoScaleR 函数。 RevoScaleR 函数表示为**rx**或**Rx**前缀以使它们以便于识别。

+ RevoScaleR 用作的分布式的数据科学的平台。 例如，你可以使用 RevoScaleR 计算上下文和转换与最先进的算法[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)。 你还可以使用[rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec)能够并行运行基础 R 函数。

RevoScaleR 操作中的示例，请参阅下列博客： 

+ [生成和部署使用 R 和 SQL Server 的预测模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [每秒含机器学习服务器一百万个预测](https://blogs.msdn.microsoft.com/mlserver/2017/10/15/1-million-predictionssec-with-machine-learning-server-web-service/)

+ [预测 taxi 提示使用 MicrosoftML](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/01/17/predicting-nyc-taxi-tips-using-microsoftml/)

+ [使用 rxExec 优化性能](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/11/14/performance-optimization-when-using-rxexec-to-parallelize-algorithms/)

## <a name="how-to-get-revoscaler"></a>如何获取 RevoScaleR

R RevoScaleR 包免费安装在 Microsoft R 客户端。 如果你有机器学习服务器或者使用 SQL Server 中的 R，默认情况下包含 RevoScaleR。

如果你使用 Python， [revoscalepy](../python/what-is-revoscalepy.md)包提供等效的功能。

> [!IMPORTANT]
> 无法下载或独立于的产品和提供它的服务使用 RevoScaleR 包。

## <a name="use-revoscaler-in-sql-server"></a>在 SQL Server 中使用 RevoScaleR

这些教程和示例演示如何使用 RevoScaleR 函数从 SQL Server 中获取数据、 生成模型，并将模型保存到数据库以获得评分。

+ [了解如何使用计算上下文](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [SQL 开发人员的 R： 训练和具有可操作性模型](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [在 GitHub 上的 Microsoft 产品示例](https://github.com/Microsoft/SQL-Server-R-Services-Samples)

## <a name="learn-more-about-revoscaler"></a>了解有关 RevoScaleR 的详细信息

这些教程演示如何在支持的其他计算上下文中使用 RevoScaleR[机器学习服务器](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)，包括 Hadoop。

+ [什么是 RevoScaleR？](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-revoscaler)

+ [浏览 RevoScaleR 在 25 函数中](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)

+ [RevoScaleR 包引用](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)

