---
title: R 教程
titleSuffix: SQL machine learning
description: 本文介绍适用于 SQL 机器学习的 R 教程。 了解如何运行脚本和构建机器学习模型。
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: cawrites
ms.author: chadam
ms.reviewer: garye, davidph
ms.date: 05/04/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 63c271c4e1d59c9446495607b42b0b5ad13ea246
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606912"
---
# <a name="r-tutorials-for-sql-machine-learning"></a>适用于 SQL 机器学习的 R 教程

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
本文介绍适用于 [SQL Server 上的机器学习服务](../sql-server-machine-learning-services.md)和[大数据群集上的机器学习服务](../../big-data-cluster/machine-learning-services.md)的 R 教程和快速入门。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
本文介绍了 [SQL Server 机器学习服务](../sql-server-machine-learning-services.md)的 R 教程和快速入门。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
本文介绍了适用于 [SQL Server 2016 R Services](../r/sql-server-r-services.md) 的 R 教程和快速入门。
::: moniker-end

<a name="bkmk_sqltutorials"></a>

## <a name="r-tutorials"></a>R 教程

| 教程 | 说明 |
|------|-------------|
| [使用决策树预测雪橇租赁](r-predictive-model-introduction.md) | 使用 R 和决策树模型预测将来的雪橇租赁数量。 在 Azure Data Studio 中使用笔记本准备数据并培训模型，并使用 T-SQL 进行模型部署。 |
| [使用 k-means 聚类分析对客户进行分类](r-clustering-model-introduction.md) | 使用 R 开发和部署 K-Means 聚类分析模型，对客户进行分类。 在 Azure Data Studio 中使用笔记本准备数据并培训模型，并使用 T-SQL 进行模型部署。 |
| [适用于数据科学家的数据库内 R 分析](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | 对于刚接触 SQL Server 的 R 开发者，本教程介绍了如何在 SQL Server 中执行常见的数据科学任务。 加载和可视化数据，定型模型并将其保存到 SQL Server，以及使用模型进行预测分析。 |
| [适用于 SQL 开发者的数据库内 R 分析](../tutorials/sqldev-in-database-r-for-sql-developers.md) | 仅使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 工具来生成并部署一个完整的解决方案。 重点介绍如何将解决方案移动到生产环境中。 学习如何将 R 代码包含在存储过程中，将 R 模型保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中，以及参数化调用 R 模型用于预测。 |

## <a name="r-quickstarts"></a>R 快速入门

如果不熟悉 SQL 机器学习，还可以尝试 R 快速入门。

| 快速入门 | 说明 |
|-|-|
| [运行简单的 R 脚本](quickstart-r-create-script.md) | 了解有关如何使用 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 在 T-SQL 中调用 R 的基础知识。 |
| [使用 R 的数据结构和对象](quickstart-r-data-types-and-objects.md) | 展示了 SQL 如何使用 R 处理数据结构。 |
| [在 R 中创建预测模型并对其进行评分](quickstart-r-data-types-and-objects.md) | 说明如何创建、训练和使用 R 模型，以根据新数据进行预测。 |

## <a name="next-steps"></a>后续步骤

有关 SQL Server 中的 R 的更多技术详细信息，请参阅 [SQL Server 中的 R 语言扩展](../concepts/extension-r.md)。
