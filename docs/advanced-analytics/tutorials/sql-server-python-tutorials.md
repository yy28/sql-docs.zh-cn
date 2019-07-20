---
title: SQL Server 2017 Python 教程概述
description: SQL Server 2017 数据库内分析的 Python 教程简介。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 86c5eaa600da0dbe9106278dd36b21eba322e2b7
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345962"
---
# <a name="sql-server-2017-python-tutorials"></a>SQL Server 2017 Python 教程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍针对[SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)上的数据库内分析的 Python 教程。 

+ 了解如何在存储过程中包装和运行 Python 代码。
+ 将基于 Python 的模型序列化并保存到 SQL Server 的数据库。
+ 了解远程和本地计算上下文以及何时使用它们。
+ 探索用于数据科学和机器学习任务的 Microsoft Python 模块。

<a name="bkmk_pythontutorials"></a>

## <a name="python-quickstarts-and-tutorials"></a>Python 快速入门和教程

| 链接 | 描述 |
|------|-------------|
| [起步SQL Server 中的 "Hello world" Python 脚本](quickstart-python-run-using-t-sql.md) | 了解如何在 T-sql 中调用 Python 的基本知识。 |
| [起步使用中的存储过程创建、定型和使用 Python 模型 SQL Server](quickstart-python-train-score-in-tsql.md) | 说明在存储过程中嵌入 Python 代码、提供输入和存储过程执行的机制。 |
| [教程：使用 revoscalepy 创建模型](use-python-revoscalepy-to-create-model.md) | 演示如何使用 SQL Server 计算上下文从远程 Python 终端运行代码。 你应该对 Python 工具和环境有一定的了解。 提供了示例代码, 该代码使用**rxLinMod**从新的**revoscalepy**库创建模型。 |
| [教程：了解面向 SQL 开发人员的数据库内 Python 分析](sqldev-in-database-python-for-sql-developers.md) | 本端到端演练演示了使用 T-sql 存储过程构建完整 Python 解决方案的过程。 所有 Python 代码都包括在内。|

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>代码示例

SQL Server 开发团队提供的这些示例和演示突出显示了在实际应用程序中使用嵌入分析的方式。

| 链接 | 描述 |
|------|-------------|
| [使用 Python 和 SQL Server 构建预测模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | 了解滑雪租赁企业如何使用机器学习来预测未来的租金, 这有助于业务计划和员工满足未来需求。 |
| [使用 Python 和 SQL Server 执行客户群集](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | 了解如何使用 Kmeans 算法来执行客户的无人监督群集。 |

## <a name="see-also"></a>请参阅

+ [要 SQL Server 的 Python 扩展](../concepts/extension-python.md)
+ [SQL Server 机器学习服务教程](machine-learning-services-tutorials.md)
