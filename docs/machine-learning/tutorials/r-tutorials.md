---
title: R 教程
description: 本文介绍了 SQL Server 机器学习服务的 R 教程和快速入门。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/13/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 952a33eb5a160acae44b5d1ae674c75b8d74cca5
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487269"
---
# <a name="r-tutorials-for-sql-server-machine-learning-services"></a>SQL Server 机器学习服务的 R 教程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍了 [SQL Server 机器学习服务](../sql-server-machine-learning-services.md)的 R 教程和快速入门。

+ 了解如何运行 R 脚本。
+ 生成和训练 R 模型，并将它部署到 SQL Server。
+ 了解远程和本地计算上下文。
+ 了解用于数据科学和机器学习的 Microsoft R 包。

<a name="bkmk_sqltutorials"></a>

## <a name="r-quickstarts-and-tutorials"></a>R 快速入门和教程

| 链接 | 说明 |
|------|-------------|
| [快速入门：创建并运行简单的 R 脚本](quickstart-r-create-script.md) | 本快速入门是几个快速入门教程中的第一个，其中演示了使用 T-SQL 查询编辑器（如 SQL Server Management Studio）调用 R 函数的基本语法。 |
| [教程：了解适用于数据科学家的数据库内 R 分析](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | 对于刚接触 SQL Server 的 R 开发者，本教程介绍了如何在 SQL Server 中执行常见的数据科学任务。 加载和可视化数据，定型模型并将其保存到 SQL Server，以及使用模型进行预测分析。 |
| [教程：了解适用于 SQL 开发者的数据库内 R 分析](../tutorials/sqldev-in-database-r-for-sql-developers.md) | 仅使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 工具来生成并部署一个完整的解决方案。 重点介绍如何将解决方案移动到生产环境中。 学习如何将 R 代码包含在存储过程中，将 R 模型保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中，以及参数化调用 R 模型用于预测。 |
| [教程：RevoScaleR 深入了解](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) | 了解如何使用 RevoScaleR 包中的函数。 在 R 和 SQL Server 之间移动数据，并切换计算上下文以适应特定的任务。 创建一些模型和图形，并将其在开发环境和数据库服务器之间进行移动。 |

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>代码示例

| 链接 | 说明 |
|------|-------------|
| [使用 R 和 SQL Server 生成预测模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | 介绍雪橇租赁公司可如何使用机器学习来预测未来的租赁情况，这有助于合理制定业务和人员计划以满足未来的需求。 |
| [使用 R 和 SQL Server 执行客户聚类分析](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | 使用无人监督学习根据销售数据细分客户。 |

## <a name="see-also"></a>另请参阅

+ [R 扩展到 SQL Server](../concepts/extension-r.md)