---
title: R 和 Python 机器学习文档-SQL Server 机器学习服务
description: R 和 Python 位于 SQL Server 中，使用内置的数据科学建模和机器学习算法进行大规模的企业数据分析。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 16bf39172144b17b3ecb03969244f31ac4715400
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962307"
---
# <a name="sql-server-machine-learning-services"></a>SQL Server 机器学习服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

## <a name="sql-server-machine-learning-services-r-and-python-documentation"></a>SQL Server 机器学习服务 （R 和 Python） 文档

了解如何通过我们的快速入门、教程和操作方法文章，在常驻的关系数据上使用 R 和 Python 外部库和语言。 中的 R 和 Python 库[SQL Server 机器学习服务](what-is-sql-server-machine-learning.md)包括基本分布、 数据科学模型、 机器学习算法和函数且不会执行大规模的高性能分析在网络上传输数据。

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
> [!NOTE]
> 有关 Java 的文档，请参阅[SQL Server 语言扩展文档](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview)。
::: moniker-end

|   |   |
|---|:--|
| ![R 徽标](media/index/logo_r.png) | 开源 R，使用 [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) 和 [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package) 中的 Microsoft AI 算法扩展。 这些库提供预测和预测模型、统计分析、可视化效果和大规模的数据操作。<br/>R 集成在 [SQL Server 2016](install/sql-r-services-windows-install.md) 中启动，也可以在 [SQL Server 2017](install/sql-machine-learning-services-windows-install.md) 中启动。 |
| ![Python 徽标](media/index/logo_python.png) | Python 开发人员可以使用 Microsoft [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) 和 [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) 进行预测分析和大规模的机器学习。 Anaconda 和 Python 3.5 兼容库为基线分发。<br/>Python 集成在 [SQL Server 2017](install/sql-machine-learning-services-windows-install.md) 中启动。 |
| &nbsp; | &nbsp; |

## <a name="5-minute-quickstarts"></a>5 分钟快速入门

- [在 R 中创建预测模型](tutorials/rtsql-create-a-predictive-model-r.md)

- [使用 R 通过模型预测和绘图](tutorials/rtsql-predict-and-plot-from-model.md)

## <a name="step-by-step-tutorials"></a>分步教程

- [如何安装到 SQL Server 机器学习服务](install/sql-machine-learning-services-windows-install.md)

- [如何从 T-SQL 和存储过程执行 R](tutorials/sqldev-in-database-r-for-sql-developers.md)

- [如何在 Python 中使用嵌入式分析](tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="video-introduction"></a>视频简介

> [!VIDEO https://www.youtube.com/embed/ACejZ9optCQ]

## <a name="reference"></a>参考

| package | 语言 | 描述 |
|:--------|:---------|:------------|
| [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) | R | R 任务的分布式和并行处理：数据转换、浏览、可视化效果、统计和预测分析。 |
| [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package) | R | 函数基于 Microsoft 的 AI 算法，适用于 R。 |
| [olapR](/machine-learning-server/r-reference/olapr/olapr) | R | 从 OLAP 多维数据集导入数据。 |
| [sqlRUtils](/machine-learning-server/r-reference/sqlrutils/sqlrutils) | R | 用于封装 R 和 T-SQL 的帮助程序函数。 |
[revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | Python | Python 任务的分布式和并行处理：数据转换、浏览、可视化效果、统计和预测分析。 |
| [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) | Python | 函数基于 Microsoft 的 AI 算法，适用于 Python。 |
| &nbsp; | &nbsp; | &nbsp; |
