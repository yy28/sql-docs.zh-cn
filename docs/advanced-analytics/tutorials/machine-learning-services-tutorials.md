---
title: SQL Server R 和 Python 教程
description: SQL Server 机器学习服务中的 R 和 Python 脚本的示例和教程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 9a212160c17e4cc3c8322af6026c9e2e4df97254
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343609"
---
# <a name="sql-server-machine-learning-tutorials-in-r-and-python"></a>R 和 Python 中的 SQL Server 机器学习教程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供了教程和代码示例的完整列表, 演示[SQL Server 2016 R 服务](../install/sql-r-services-windows-install.md)或[SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)的机器学习功能。 

+ 快速入门使用内置数据或不使用任何数据进行快速探索。
+ 教程更深入地介绍了更多任务、更大的数据集和更多的解释。
+ 示例和解决方案适用于想要从代码开始的开发人员, 可通过向后翻到概念和教训来填补知识缺口。

你将了解如何在同一操作上下文中使用带有常驻关系数据的 R 和 Python 库, 如何使用 SQL Server 存储过程来运行和部署自定义代码, 以及如何为高性能数据调用 Microsoft R 和 Python 库科学和机器学习任务。

作为第一步, 请查看支持 Microsoft R 和 Python 与 SQL Server 集成的基础概念。

## <a name="concepts"></a>概念

数据库内分析是指在将 SQL Server 机器学习服务或 SQL Server 2016 R Services (仅 R) 作为数据库引擎的外接程序安装时 SQL Server 上对 R 和 Python 的本机支持。 R 和 Python 集成包括基本开源分发版, 以及用于高性能分析的 Microsoft 特定库。

从体系结构的一个位置来, 你的代码将作为外部进程运行, 以保留数据库引擎的完整性。 但是, 所有数据访问和安全性都是通过 SQL Server 数据库角色和权限来完成的, 这意味着有权访问 SQL Server 的任何应用程序都可以在将 R 和 Python 脚本作为存储过程进行部署时访问 R 和 Python 脚本, 或者将定型模型序列化并保存到 SQL服务器数据库。

SQL Server 上的 R 和 Python 支持与其他 Microsoft 产品和服务中的等效语言支持之间的主要区别包括:

+ 能够在存储过程中或作为二进制模型 "打包" 代码。
+ 编写用于调用本地安装的 Microsoft R 和 Python 库的代码, 并附带 SQL Server 的程序文件。
+ 将 SQL Server 的数据库安全体系结构应用于 R 和 Python 解决方案。
+ 利用 SQL Server 基础结构和对自定义解决方案的管理支持。

## <a name="quickstarts"></a>快速入门

从这里开始了解如何从 T-sql 运行 R 或 Python, 以及如何为 SQL 生产环境操作 R 和 Python 代码。

+ [Python使用 T-sql 运行 Python](run-python-using-t-sql.md)
+ [迅驰R 和 SQL 中的 Hello World](rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [迅驰处理输入和输出](rtsql-working-with-inputs-and-outputs.md)
+ [迅驰处理数据类型和对象](rtsql-r-and-sql-data-types-and-data-objects.md)
+ [迅驰使用 R 函数](rtsql-using-r-functions-with-sql-server-data.md)
+ [迅驰创建预测模型](rtsql-create-a-predictive-model-r.md)
+ [迅驰从模型预测和绘图](rtsql-predict-and-plot-from-model.md)

## <a name="tutorials"></a>教程

通过更深入地了解 Microsoft 包和更具体的操作 (如从本地到远程计算上下文的转换), 在首次使用 R、Python 和 T-sql 时进行构建。

+ [Python 教程](sql-server-python-tutorials.md)
+ [R 教程](sql-server-r-tutorials.md)

<a name ="bkmk_samples"></a>

## <a name="samples"></a>示例

SQL Server 和 R Server 开发团队提供的这些示例和演示突出显示了在实际应用程序中使用嵌入分析的方式。

| 链接 | 描述 | 
|------|-------------|
| [使用 R 和 SQL Server 执行客户群集](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | 使用无人监督 learning 基于销售数据对客户进行细分。 此示例使用 Microsoft R 中的可伸缩 rxKmeans 算法生成聚类分析模型。 |
| [使用 Python 和 SQL Server 执行客户群集](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | 了解如何使用 Kmeans 算法来执行客户的无人监督群集。 此示例使用数据库中的 Python 语言。| SQL Server 2017 |
| [使用 R 和 SQL Server 构建预测模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | 了解滑雪租赁企业如何使用机器学习来预测未来的租金, 这有助于业务计划和员工满足未来需求。 此示例使用 Microsoft 算法生成逻辑回归和决策树模型。 | 
| [使用 Python 和 SQL Server 构建预测模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | 使用 Python 构建 ski 租赁分析应用程序, 帮助规划未来需求。 此示例使用新的 Python 库**revoscalepy**创建线性回归模型。 | 

<a name="bkmk_solutions"></a>

## <a name="solution-templates"></a>解决方案模板

Microsoft 数据科学团队提供了可自定义的解决方案模板, 可用于常见方案的快速启动解决方案。 每个解决方案都针对特定的任务或行业问题进行定制。 大多数解决方案都设计为在 SQL Server 或云环境 (如 Azure 机器学习) 中运行。 其他解决方案可通过使用 Microsoft R Server 或 Machine Learning Server 在 Linux 或 Spark 或 Hadoop 群集中运行。

提供了所有代码, 以及有关如何使用 SQL Server 存储过程为评分定型和部署模型的说明。

+ [欺诈检测](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [自定义改动预测](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [预测维护](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [预测医院时长](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

