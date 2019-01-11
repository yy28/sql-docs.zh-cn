---
title: R 和 Python 机器学习和编程扩展文档 - SQL Server 机器学习
description: R 和 Python 位于 SQL Server 中，使用内置的数据科学建模和机器学习算法进行大规模的企业数据分析。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/09/2019
ms.topic: overview
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 7eb5083f17ab08f19b689b3550f979f88495f604
ms.sourcegitcommit: 1f53b6a536ccffd701fc87e658ddac714f6da7a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2019
ms.locfileid: "54206243"
---
# <a name="sql-server-machine-learning"></a>SQL Server 机器学习

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"

## <a name="sql-server-machine-learning-and-programming-extensions-documentation"></a>SQL Server 机器学习和编程扩展文档

了解如何通过我们的快速入门、教程和操作方法文章，在常驻的关系数据上使用 R 和 Python 外部库和语言。 R 和 Python 库位于 [SQL Server 机器学习](what-is-sql-server-machine-learning.md)中，包括基本分布、数据科学模型、机器学习算法和函数，用于进行大规模高性能分析，而无需跨网络传输数据。 

在 SQL Server 2019 中，Java 代码执行使用相同的可扩展性框架作为 R 和 Python，但不包括数据科学和机器学习函数库。 有关新功能的详细信息，请参阅 [SQL Server 机器服务中的新增功能](what-s-new-in-sql-server-machine-learning-services.md)。

|   |   | 
|---|---|-
| ![R 徽标](./media/index/logo_r.png) | 开源 R，使用 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 和 [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) 中的 Microsoft AI 算法扩展。 这些库提供预测和预测模型、统计分析、可视化效果和大规模的数据操作。 <br/>R 集成在 [SQL Server 2016](./install/sql-r-services-windows-install.md) 中启动，也可以在 [SQL Server 2017](./install/sql-machine-learning-services-windows-install.md) 中启动。 | 
| ![Python 徽标](./media/index/logo_python.png) | Python 开发人员可以使用 Microsoft [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) 和 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 进行预测分析和大规模的机器学习。 Anaconda 和 Python 3.5 兼容库为基线分发。 <br/>Python 集成在 [SQL Server 2017](./install/sql-machine-learning-services-windows-install.md) 中启动。  | 
| ![Java 徽标](./media/index/logo_java.png) | Java 开发人员可以使用 [Java 语言扩展](java/extension-java.md)在存储过程中包装代码，或者采用可通过 Transact-SQL 访问的二进制格式。 <br/>Java 集成在 [SQL Server 2019 - 预览版](./install/sql-machine-learning-services-ver15.md)中启动。 |
::: moniker-end

::: moniker range="=sql-server-2016||=sql-server-2017"

## <a name="sql-server-machine-learning-r-and-python-documentation"></a>SQL Server 机器学习 R 和 Python 文档

了解如何通过我们的快速入门、教程和操作方法文章，在常驻的关系数据上使用 R 和 Python 外部库和语言。 R 和 Python 库位于 [SQL Server 机器学习](what-is-sql-server-machine-learning.md)中，包括基本分布、数据科学模型、机器学习算法和函数，用于进行大规模高性能分析，而无需跨网络传输数据。 

|   |   | 
|---|---|-
| ![R 徽标](./media/index/logo_r.png) | 开源 R，使用 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 和 [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) 中的 Microsoft AI 算法扩展。 这些库提供预测和预测模型、统计分析、可视化效果和大规模的数据操作。 <br/>R 集成在 [SQL Server 2016](./install/sql-r-services-windows-install.md) 中启动，也可以在 [SQL Server 2017](./install/sql-machine-learning-services-windows-install.md) 中启动。 | 
| ![Python 徽标](./media/index/logo_python.png) | Python 开发人员可以使用 Microsoft [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) 和 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 进行预测分析和大规模的机器学习。 Anaconda 和 Python 3.5 兼容库为基线分发。 <br/>Python 集成在 [SQL Server 2017](./install/sql-machine-learning-services-windows-install.md) 中启动。  | 
::: moniker-end

## <a name="5-minute-quickstarts"></a>5 分钟快速入门

+ [在 R 中创建预测模型](./tutorials/rtsql-create-a-predictive-model-r.md)

+ [使用 R 通过模型预测和绘图](./tutorials/rtsql-predict-and-plot-from-model.md)


## <a name="step-by-step-tutorials"></a>分步教程

+ [如何将机器学习和可扩展性框架添加到 SQL Server](install/sql-machine-learning-services-windows-install.md)

+ [如何从 T-SQL 和存储过程执行 R](./tutorials/sqldev-in-database-r-for-sql-developers.md)

+ [如何在 Python 中使用嵌入式分析](./tutorials/sqldev-in-database-python-for-sql-developers.md)


## <a name="video-introduction"></a>视频简介

> [!VIDEO https://www.youtube.com/embed/ACejZ9optCQ]

## <a name="reference"></a>参考

| “包” | “报表” | 描述 | 
|---------|----------|-------------|
| [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | R | R 任务的分布式和并行处理：数据转换、浏览、可视化效果、统计和预测分析。 |
| [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | R | 函数基于 Microsoft 的 AI 算法，适用于 R。 |
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | R | 从 OLAP 多维数据集导入数据。 |
| [sqlRUtils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | R | 用于封装 R 和 T-SQL 的帮助程序函数。 |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | Python | Python 任务的分布式和并行处理：数据转换、浏览、可视化效果、统计和预测分析。  | 
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | Python | 函数基于 Microsoft 的 AI 算法，适用于 Python。  |