---
title: SQL Server R 教程概述
description: 介绍 SQL Server 数据库内分析的 R 语言教程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ff1027a3a791ef0151e61982445cafff7be40329
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715425"
---
# <a name="sql-server-r-language-tutorials"></a>SQL Server R 语言教程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍针对[SQL Server 2016 R 服务](../install/sql-r-services-windows-install.md)或[SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)上的数据库内分析的 R 语言教程。

+ 了解如何在存储过程中包装和运行 R 代码。
+ 将基于 r 的模型序列化并保存到 SQL Server 的数据库。
+ 了解远程和本地计算上下文以及何时使用它们。
+ 探索用于数据科学和机器学习任务的 Microsoft R 库。

<a name="bkmk_sqltutorials"></a>

## <a name="r-quickstarts-and-tutorials"></a>R 快速入门和教程

| 链接 | 描述 |
|------|-------------|
| [起步在 T-sql 中使用 R](rtsql-using-r-code-in-transact-sql-quickstart.md) | 首先, 使用这一快速入门教程, 其中演示了使用 T-sql 查询编辑器 (如 SQL Server Management Studio) 调用 R 函数的基本语法。 |
| [教程：了解数据科学家的数据库内 R 分析](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | 本教程介绍了如何在 SQL Server 中执行常见 SQL Server 的数据科学任务。 加载和可视化数据, 定型模型并将其保存到 SQL Server, 并使用模型进行预测分析。 |
| [教程：了解适用于 SQL 开发人员的数据库内 R 分析](../tutorials/sqldev-in-database-r-for-sql-developers.md) | 只[!INCLUDE[tsql](../../includes/tsql-md.md)]使用工具生成并部署一个完整的 R 解决方案。 重点介绍如何将解决方案移动到生产环境中。 学习如何将 R 代码包含在存储过程中，将 R 模型保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中，以及参数化调用 R 模型用于预测。 |
| [教程：RevoScalepR 深入探讨](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) | 了解如何使用 RevoScaleR 包中的函数。 在 R 和 SQL Server 之间移动数据, 并切换计算上下文以适应特定的任务。 创建模型和绘图, 并在开发环境和数据库服务器之间移动它们。 |

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>代码示例

| 链接 | 描述 |
|------|-------------|
| [使用 R 和 SQL Server 构建预测模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | 了解滑雪租赁企业如何使用机器学习来预测未来的租金, 这有助于业务计划和员工满足未来需求。 |
| [使用 R 和 SQL Server 执行客户群集](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | 使用无人监督 learning 基于销售数据对客户进行细分。 |

## <a name="see-also"></a>请参阅

+ [要 SQL Server 的 R 扩展](../concepts/extension-r.md)
+ [SQL Server 机器学习服务教程](machine-learning-services-tutorials.md)

