---
title: SQL Server 2017 Python 教程概述-SQL Server 机器学习
description: Python 教程： SQL Server 2017 数据库内分析的简介。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f5dab603a7295009bee5275b721e987d5de76710
ms.sourcegitcommit: ad3b2133585bc14fc6ef8be91f8b74ee2f498b64
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2019
ms.locfileid: "56425782"
---
# <a name="sql-server-2017-python-tutorials"></a>SQL Server 2017 Python 教程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍有关在数据库内分析的 Python 教程[SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)。 

+ 了解如何自动换行和存储过程中运行 Python 代码。
+ 序列化并将基于 Python 的模型保存到 SQL Server 数据库。
+ 了解有关远程和本地计算上下文，以及何时使用它们。
+ 探索数据科学和机器学习任务的 Microsoft Python 模块。

<a name="bkmk_pythontutorials"></a>

## <a name="python-quickstarts-and-tutorials"></a>Python 快速入门和教程

| 链接 | Description |
|------|-------------|
| [快速入门：SQL Server 中的"hello world"Python 脚本](quickstart-python-run-using-t-sql.md) | 了解如何在 T-SQL 中调用 Python 的基础知识。 |
| [快速入门：创建、 定型和 SQL Server 中使用存储过程中使用 Python 模型](quickstart-python-train-score-in-tsql.md) | 介绍了在提供输入和存储的过程执行的存储过程中嵌入 Python 代码的机制。 |
| [教程：使用 revoscalepy 创建模型](use-python-revoscalepy-to-create-model.md) | 演示如何从远程 Python 终端中，使用 SQL Server 计算上下文中运行代码。 应为一定程度上熟悉的 Python 工具和环境。 提供用于创建模型使用的示例代码， **rxLinMod**，从新建**revoscalepy**库。 |
| [教程：面向 SQL 开发人员了解数据库内 Python 分析](sqldev-in-database-python-for-sql-developers.md) | 本端到端演练演示如何构建完整的 Python 解决方案使用 T-SQL 存储过程的过程。 包含所有 Python 代码都。|

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>代码示例

这些示例和演示 SQL Server 开发团队提供的突出显示您可以在实际应用程序中使用嵌入式的分析方法。

| 链接 | Description |
|------|-------------|
| [构建预测模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | 介绍了雪橇租赁公司如何使用机器学习来预测未来的租赁情况，可帮助业务和人员计划以满足未来的需求。 |
| [执行客户使用 Python 和 SQL Server 聚类分析](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | 了解如何使用 k 均值算法执行无人监督聚类分析的客户。 |

## <a name="see-also"></a>另请参阅

+ [到 SQL Server 的 Python 扩展](../concepts/extension-python.md)
+ [SQL Server 机器学习服务教程](machine-learning-services-tutorials.md)
