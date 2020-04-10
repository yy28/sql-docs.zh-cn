---
title: R 教程
description: 介绍 SQL Server 数据库内分析的 R 语言教程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 62264f728fec5b68c3034fb3c6260f04617353b5
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116110"
---
# <a name="sql-server-r-language-tutorials"></a>SQL Server R 语言教程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍了用于在 [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) 或 [SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)上进行数据库内分析的 R 语言教程。

+ 了解如何在存储过程中包装和运行 R 代码。
+ 将基于 R 的模型序列化并保存到 SQL Server 数据库。
+ 了解远程和本地计算上下文以及何时使用它们。
+ 探索用于数据科学和机器学习任务的 Microsoft R 库。

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