---
title: "SQL Server 机器学习服务教程 |Microsoft 文档"
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- Python
- R
ms.assetid: 5ccc75f6-6703-47d9-b879-9a740569b45e
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 8631ebd8cee2eb5f94fd1c28bee71f9fcfee192f
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2018
---
# <a name="tutorials-for-sql-server-machine-learning-services"></a>有关 SQL Server 计算机学习 Services 教程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供教程、 演示和示例应用程序使用 SQL Server 2016 或 SQL Server 2017 机器学习功能的完整的列表。 从这里开始，若要了解如何从 T-SQL 运行 R 或 Python、 如何使用远程和本地计算上下文和如何优化 SQL 生产环境中 R 和 Python 代码。

## <a name="start-here"></a>起点

+ [Python 教程](../tutorials/sql-server-python-tutorials.md)

+ [R 教程](../tutorials/sql-server-r-tutorials.md)

有关要求以及如何进行设置的详细信息，请参阅[先决条件](#bkmk_prerequisites)。

## <a name="samples-and-solutions"></a>示例和解决方案

+ [示例](#bkmk_samples) 

    SQL Server 开发团队的以下实际方案演示如何在应用程序中嵌入机器学习。 所有示例都包括在生产环境中你可以下载、 修改和使用的代码。

+ [解决方案](#bkmk_solutions) 

    从 Microsoft 数据科学团队的模板是可自定义以帮助你快速入门机器学习。 每个解决方案量身定制的具体任务或行业问题。 大部分的解决方案用于 SQL Server 或 Azure 机器学习等云环境中运行。 其他解决方案可以通过使用 Microsoft R Server 或机器学习服务器运行在 Linux 上或在 Spark 或 Hadoop 群集中。

### <a name ="bkmk_samples"></a>SQL Server 产品示例

这些示例和演示 SQL Server 和 R Server 开发团队提供的突出显示实际的应用程序中使用嵌入的分析的方式。

+ [执行客户群集使用 R 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/)

  使用无人监督的学习到段客户基于销售数据。 此示例使用从 Microsoft R 可缩放 rxKmeans 算法生成聚类分析模型。 
  
  适用于： SQL Server 2016 或 SQL Server 自 2017 年 1

+ [新增功能！执行客户群集使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    了解如何使用 Kmeans 算法来执行无人监督聚类分析的客户。 此示例使用 Python 语言数据库中。
    
    适用于： SQL Server 自 2017 年 1

+ [生成使用 R 和 SQL Server 的预测模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction)

  了解如何 ski 租赁业务可能使用机器学习来预测将来出租，它可帮助企业版计划和员工，以满足将来需求。 此示例中使用的 Microsoft 算法生成逻辑回归和决策树模型。 
  
  适用于： SQL Server 2016 或 SQL Server 自 2017 年 1

+ [构建预测模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

   生成 ski 租赁分析应用程序使用 Python，以帮助你规划将来的需求。 此示例使用新的 Python 库**revoscalepy**，若要创建线性回归模型。
   
   适用于： SQL Server 自 2017 年 1

+ [如何使用 SQL Server 计算机学习 Services Tableau](https://blogs.msdn.microsoft.com/mlserver/2017/12/14/how-to-use-tableau-with-sql-server-machine-learning-services-with-r-and-python/)

    分析社交媒体和创建 Tableau 关系图，使用 SQL Server 和。

### <a name="bkmk_solutions"></a>解决方案模板

Microsoft 数据科学团队提供的解决方案模板，可以使用可快速开发解决方案的常见方案。 提供的所有代码，以及关于如何训练和部署的模型评分使用 SQL Server 存储过程的说明。

+ [欺诈检测](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [自定义改动预测](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [预测维护](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [预测保持状态的医院长度](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

有关详细信息，请参阅 [Machine Learning Templates with SQL Server 2016 R Services](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/)（具有 SQL Server 2016 R Services 的机器学习模板）。

## <a name="more-resources-and-reading"></a>更多资源和读取

+ [我们为何未生成它？](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/01/10/sql-server-r-services-why-did-we-build-it/)

    想要了解 R Services 背后的真实故事吗？ 从开发和说明的源和目标 SQL Server R Services 的 PM 团队阅读这篇文章。

+ [教程和 Microsoft R 的示例数据](https://docs.microsoft.com/machine-learning-server/r/tutorial-introduction)

    了解有关 Microsoft R 和 RevoScaleR 包所提供的功能的快速教程的此集合中。 了解如何编写 R 代码一次和部署任何位置，使用 RevoScaleR 数据源和远程计算上下文。

+ [要开始使用 MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)

  了解如何对高级的建模和可伸缩性数据转换，针对多个计算上下文优化 MicrosoftML 包中使用新的算法。

## <a name="bkmk_Prerequisites"></a>先决条件

若要运行这些教程，必须下载并安装 SQL Server 机器学习组件，如下所述：

+ [安装 SQL Server 自 2017 年 1 机器学习 Services （数据库）](../install/sql-machine-learning-services-windows-install.md)
+ [安装 SQL Server 2016 R Services （数据库）](../install/sql-r-services-windows-install.md)

使用 SQL Server 自 2017 年，你可以安装 R 和 / 或 Python。 否则总体的安装过程、 体系结构和要求是相同的。

运行 SQL Server 安装程序之后, 不要忘记以下重要步骤：

1. 通过运行启用外部脚本执行功能`sp_configure 'external scripts enabled', 1`。 按照说明重新配置并重新启动 SQL Server。
2. 请确保： 快速启动板服务正在运行，且快速启动板辅助帐户可以连接到 SQL Server 实例。
3. 查看与必须运行 R 或 Python 脚本的用户关联的权限。 无论使用 SQL 登录名或 Windows 用户帐户，用户必须有权运行 R 或 Python 脚本，并且必须能够连接到的实例。 根据教程中，用户可能还需要权限来写入数据、 创建数据库对象，或执行大容量导入的数据。

有关详细信息，请参阅有关的一些常见问题设置和配置此文章：[疑难解答机器学习服务](../machine-learning-troubleshooting-faq.md)

> [!NOTE]
> 无法运行这些教程中使用另一个开放源代码 R 或 Python 工具。 你的开发环境和机器学习的 SQL Server 计算机必须具有的 R 或 Python 库 Microsoft 提供的支持与 SQL Server 和使用远程计算上下文的集成。
