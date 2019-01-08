---
title: SQL Server R 和 Python 教程-SQL Server 机器学习
description: 示例和对 R 和 Python 在 SQL Server 机器学习服务中编写脚本的教程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 69009a5a11e7f7985729656ae9df6c60bcba8037
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596928"
---
# <a name="sql-server-machine-learning-tutorials-in-r-and-python"></a>R 和 Python 中的 SQL Server 机器学习教程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供的教程和代码示例演示机器学习功能的完整列表[SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)或[SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)。 

+ 快速入门使用内置的数据或任何数据与工作量最少的快速浏览。
+ 教程深入详细任务、 大型数据集，以及更长的说明。
+ 示例和解决方案适用于开发人员面向更愿意使用的代码中，启动逆向执行概念和课程知识填补了。

您将学习如何使用 R 和 Python 库与常驻关系数据中的相同的操作上下文、 如何使用 SQL Server 存储过程来运行和部署自定义代码，以及如何调用 Microsoft R 和 Python 库，实现高性能数据科学和机器学习任务。

作为第一个步骤中，请查看支持 Microsoft 的基础概念与 SQL Server 的 R 和 Python 集成。

## <a name="concepts"></a>概念

数据库内分析是指对 R 和 Python 在 SQL Server 上的本机支持作为到数据库引擎外接程序安装 SQL Server 机器学习服务或 SQL Server 2016 R Services (仅适用于 R) 时。 R 和 Python 集成包括基本的开源分发版，以及高性能分析的特定于 Microsoft 的库。

从体系结构独立点，你的代码作为外部进程上运行相应的框以保留数据库引擎的完整性。 但是，所有数据都访问和安全性是通过 SQL Server 数据库角色和权限，这意味着任何应用程序具有访问都权限与 SQL Server 可以都访问 R 和 Python 脚本，将其部署为存储过程，或序列化并将已训练的模型保存到 SQL服务器数据库。

SQL Server 上支持与其他 Microsoft 产品中的等效语言支持的 R 和 Python 之间的主要差异，并且服务包括：

+ "包"代码的存储过程中或作为二进制模型的能力。
+ 编写调用本地和 SQL Server 程序文件一起安装的 Microsoft R 和 Python 库的代码。
+ 适用于 R 和 Python 解决方案的 SQL Server 数据库安全体系结构。
+ 利用 SQL Server 基础结构和管理支持自定义解决方案。

## <a name="quickstarts"></a>快速入门

从这里开始，若要了解如何从 T-SQL 运行 R 或 Python，以及如何将 R 和 Python 代码 SQL 生产环境中进行操作。

+ [Python:使用 T-SQL 运行的 Python](run-python-using-t-sql.md)
+ [:R 和 SQL 中的 hello World](rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [:处理输入和输出](rtsql-working-with-inputs-and-outputs.md)
+ [:处理数据类型和对象](rtsql-r-and-sql-data-types-and-data-objects.md)
+ [:使用 R 函数](rtsql-using-r-functions-with-sql-server-data.md)
+ [:创建预测模型](rtsql-create-a-predictive-model-r.md)
+ [:通过模型预测和绘图](rtsql-predict-and-plot-from-model.md)

## <a name="tutorials"></a>教程

通过执行深入研究 Microsoft 包和更多专用的操作，如从本地切换到远程计算上下文上首次体验 R 和 Python 和 T-SQL 的生成。

+ [Python 教程](sql-server-python-tutorials.md)
+ [R 教程](sql-server-r-tutorials.md)

<a name ="bkmk_samples"></a>

## <a name="samples"></a>示例

这些示例和演示 SQL Server 和 R Server 开发团队提供的突出显示您可以在实际应用程序中使用嵌入式的分析方法。

| 链接 | Description | 
|------|-------------|
| [执行客户使用 R 和 SQL Server 聚类分析](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | 使用为客户分段基于销售数据的非监督式的学习。 此示例使用 Microsoft R 中的可缩放的 rxKmeans 算法来生成聚类分析模型。 |
| [执行客户使用 Python 和 SQL Server 聚类分析](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | 了解如何使用 k 均值算法执行无人监督聚类分析的客户。 此示例中使用 Python 语言中的数据库。| SQL Server 2017 |
| [构建预测模型使用 R 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | 介绍了雪橇租赁公司如何使用机器学习来预测未来的租赁情况，可帮助业务和人员计划以满足未来的需求。 此示例中使用的 Microsoft 算法来生成逻辑回归和决策树模型。 | 
| [构建预测模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | 生成使用 Python，以帮助规划的未来需求的 ski 租赁分析应用程序。 此示例使用新的 Python 库， **revoscalepy**，以创建线性回归模型。 | 
| [如何使用 Tableau 与 SQL Server 机器学习服务](https://blogs.msdn.microsoft.com/mlserver/2017/12/14/how-to-use-tableau-with-sql-server-machine-learning-services-with-r-and-python/) | 分析社交媒体和创建 Tableau 关系图，使用 SQL Server 和。 | 

<a name="bkmk_solutions"></a>

## <a name="solution-templates"></a>解决方案模板

Microsoft 数据科学团队提供了可用于快速开始针对常见方案的解决方案的可自定义解决方案模板。 每个解决方案进行量身定制的具体任务或行业问题。 大部分解决方案旨在以在 SQL Server 或 Azure 机器学习等云环境中运行。 其他解决方案可以运行在 Linux 上或在 Spark 或 Hadoop 群集中，通过使用 Microsoft R Server 或 Machine Learning Server。

提供了所有代码，以及如何训练和部署模型用于评分使用 SQL Server 存储过程的说明。

+ [欺诈检测](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [自定义改动预测](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [预测维护](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [预测医院住院天数](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

有关详细信息，请参阅 [Machine Learning Templates with SQL Server 2016 R Services](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/)（具有 SQL Server 2016 R Services 的机器学习模板）。

