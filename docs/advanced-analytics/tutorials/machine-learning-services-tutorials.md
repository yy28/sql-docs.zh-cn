---
title: SQL Server 机器学习服务教程 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/22/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 08528f3459022bdcb97b97e22d6f6c474c31a715
ms.sourcegitcommit: eddf8cede905d2adb3468d00220a347acd31ae8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2018
ms.locfileid: "49960741"
---
# <a name="tutorials-for-sql-server-machine-learning-services"></a>有关 SQL Server 机器学习服务教程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供了全面的教程、 演示和示例应用程序使用 SQL Server 2016 或 SQL Server 2017 中的机器学习功能的列表。 从这里开始，若要了解如何从 T-SQL 运行 R 或 Python、 如何使用远程和本地计算上下文和如何将 R 和 Python 代码 SQL 生产环境中进行操作。

+ [Python 教程](../tutorials/sql-server-python-tutorials.md)

+ [R 教程](../tutorials/sql-server-r-tutorials.md)

## <a name ="bkmk_samples"></a>R 和 Python 示例

这些示例和演示 SQL Server 和 R Server 开发团队提供的突出显示您可以在实际应用程序中使用嵌入式的分析方法。

| 链接 | Description | 适用于 |
|------|-------------|------------|
| [执行客户使用 R 和 SQL Server 聚类分析](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | 使用为客户分段基于销售数据的非监督式的学习。 此示例使用 Microsoft R 中的可缩放的 rxKmeans 算法来生成聚类分析模型。 | SQL Server 2016 或 SQL Server 2017 |
| [执行客户使用 Python 和 SQL Server 聚类分析](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | 了解如何使用 k 均值算法执行无人监督聚类分析的客户。 此示例中使用 Python 语言中的数据库。| SQL Server 2017 |
| [构建预测模型使用 R 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | 介绍了雪橇租赁公司如何使用机器学习来预测未来的租赁情况，可帮助业务和人员计划以满足未来的需求。 此示例中使用的 Microsoft 算法来生成逻辑回归和决策树模型。 | SQL Server 2016 或 SQL Server 2017 |
| [构建预测模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | 生成使用 Python，以帮助规划的未来需求的 ski 租赁分析应用程序。 此示例使用新的 Python 库， **revoscalepy**，以创建线性回归模型。 | SQL Server 2017 |
| [如何使用 Tableau 与 SQL Server 机器学习服务](https://blogs.msdn.microsoft.com/mlserver/2017/12/14/how-to-use-tableau-with-sql-server-machine-learning-services-with-r-and-python/) | 分析社交媒体和创建 Tableau 关系图，使用 SQL Server 和。 | SQL Server 2016 或 SQL Server 2017 |

## <a name="bkmk_solutions"></a>解决方案模板

Microsoft 数据科学团队提供了可用于快速开始针对常见方案的解决方案的可自定义解决方案模板。 每个解决方案进行量身定制的具体任务或行业问题。 大部分解决方案旨在以在 SQL Server 或 Azure 机器学习等云环境中运行。 其他解决方案可以运行在 Linux 上或在 Spark 或 Hadoop 群集中，通过使用 Microsoft R Server 或 Machine Learning Server。

提供了所有代码，以及如何训练和部署模型用于评分使用 SQL Server 存储过程的说明。

+ [欺诈检测](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [自定义改动预测](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [预测维护](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [预测医院住院天数](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

有关详细信息，请参阅 [Machine Learning Templates with SQL Server 2016 R Services](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/)（具有 SQL Server 2016 R Services 的机器学习模板）。

## <a name="recommended-reading"></a>推荐的读物

+ [我们为什么构建它？](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/01/10/sql-server-r-services-why-did-we-build-it/)

    想要了解 R Services 背后的真实故事吗？ 从开发和说明的源和目标 SQL Server R Services 的 PM 团队阅读此文章。

+ [教程和 Microsoft R 的示例数据](https://docs.microsoft.com/machine-learning-server/r/tutorial-introduction)

    了解有关 Microsoft R 和 RevoScaleR 包提供了快速教程的此集合中。 了解如何进行一次编写 R 代码并将其部署任意位置，使用 RevoScaleR 数据源和远程计算上下文。

+ [开始使用 MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)

  了解如何为高级的建模和可缩放的数据转换，针对多个计算上下文进行了优化 MicrosoftML 包中使用新的算法。
