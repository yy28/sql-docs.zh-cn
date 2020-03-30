---
title: Python 教程
description: 本文介绍 SQL Server 机器学习服务的 Python 教程。 了解如何在 SQL Server 中运行脚本和构建机器学习模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b8caa58c178f68ebcf773fcef8f18509b85ad24a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "74908748"
---
# <a name="python-tutorials-for-sql-server-machine-learning-services"></a>SQL Server 机器学习服务的 Python 教程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍 [SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)的 Python 教程和快速入门。

+ 了解如何运行 Python 脚本。
+ 构建、培训 Python 模型并将其部署到 SQL Server。
+ 了解远程和本地计算上下文。
+ 了解用于数据科学和机器学习的 Microsoft Python 包。

<a name="bkmk_pythontutorials"></a>

## <a name="python-tutorials"></a>Python 教程

| 教程 | 说明 |
|-|-|
| [使用线性回归预测雪橇租赁](python-ski-rental-linear-regression.md) | 使用 Python 和线性回归来预测滑雪租赁数量。 在 Azure Data Studio 中使用笔记本准备数据并培训模型，并使用 T-SQL 进行模型部署。 |
| [使用 k-means 聚类分析对客户进行分类](python-clustering-model.md) | 使用 Python 开发和部署 K-Means 群集模型，对客户进行分类。 在 Azure Data Studio 中使用笔记本准备数据并培训模型，并使用 T-SQL 进行模型部署。 |
| [使用 Revoscalepy 创建模型](use-python-revoscalepy-to-create-model.md) | 演示如何使用 SQL Server 作为计算上下文来运行远程 Python 客户端中的代码。 本教程使用 revoscalepy 库中的 rxLinMod 创建模型   。 |
| [适用于 SQL 开发者的 Python 数据分析](sqldev-in-database-python-for-sql-developers.md) | 本端到端演练演示使用 T-SQL 构建完整的 Python 解决方案的过程。 |

## <a name="python-quickstarts"></a>Python 快速入门

如果不熟悉 SQL Server 机器学习服务，还可以尝试 Python 快速入门。

| 快速入门 | 说明 |
|-|-|
| [Python 和 SQL Server 中的 Hello World](quickstart-python-create-script.md) | 了解关于如何使用 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 在 T-SQL 中调用 Python 的基础知识。 |
| [在 SQL Server 中使用 Python 处理数据类型和对象](quickstart-python-data-structures.md) | 演示 SQL Server 如何使用 Python pandas 包处理数据结构。 |
| [在 Python 中创建预测模型并对其进行评分](quickstart-python-train-score-model.md) | 说明如何创建、培训和使用 Python 模型，以根据新数据进行预测。 |

## <a name="next-steps"></a>后续步骤

+ [什么是 SQL Server 机器学习服务（Python 和 R）？](../what-is-sql-server-machine-learning.md)
+ [SQL Server 中的 Python 扩展](../concepts/extension-python.md)