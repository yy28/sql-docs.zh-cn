---
title: SQL Server R 教程概述-SQL Server 机器学习
description: SQL Server 数据库内分析 R 语言教程简介。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 4353d50ecfd8aac3ada1c71baf1be78f13c51b11
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596528"
---
# <a name="sql-server-r-language-tutorials"></a>SQL Server R 语言教程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍有关在数据库内分析 R 语言教程[SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)或[SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)。

+ 了解如何自动换行和存储过程中运行 R 代码。
+ 序列化并将基于 r 的模型保存到 SQL Server 数据库。
+ 了解有关远程和本地计算上下文，以及何时使用它们。
+ 探索用于数据科学和机器学习任务的 Microsoft R 库。

<a name="bkmk_sqltutorials"></a>

## <a name="r-quickstarts-and-tutorials"></a>R 快速入门和教程

| 链接 | Description |
|------|-------------|
| [快速入门：在 T-SQL 中使用 R](rtsql-using-r-code-in-transact-sql-quickstart.md) | 在一个说明调用使用诸如 SQL Server Management Studio 的 T-SQL 查询编辑器的 R 函数的基本语法的几个快速入门的第一个。 |
| [教程：为数据科学家了解数据库内 R 分析](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | 对于刚接触 SQL Server 的 R 开发人员，本教程介绍如何执行常见数据科学任务，在 SQL Server 中。 加载和可视化数据、 训练和将模型保存到 SQL Server 和使用模型进行预测分析。 |
| [教程：面向 SQL 开发人员了解数据库内 R 分析](../tutorials/sqldev-in-database-r-for-sql-developers.md) | 生成和部署一个完整的 R 解决方案，仅使用[!INCLUDE[tsql](../../includes/tsql-md.md)]工具。 重点介绍将解决方案移到生产环境。 学习如何将 R 代码包含在存储过程中，将 R 模型保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中，以及参数化调用 R 模型用于预测。 |
| [教程：RevoScalepR 深入探讨](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) | 了解如何使用 RevoScaleR 包中的函数。 R 和 SQL Server 和交换机之间移动数据计算上下文，以满足特定的任务。 创建模型和图形，并在开发环境和数据库服务器之间移动它们。 |

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>代码示例

| 链接 | Description |
|------|-------------|
| [构建预测模型使用 R 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | 介绍了雪橇租赁公司如何使用机器学习来预测未来的租赁情况，可帮助业务和人员计划以满足未来的需求。 |
| [执行客户使用 R 和 SQL Server 聚类分析](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | 使用为客户分段基于销售数据的非监督式的学习。 |

## <a name="see-also"></a>另请参阅

+ [到 SQL Server 的 R 扩展](../concepts/extension-r.md)
+ [SQL Server 机器学习服务教程](machine-learning-services-tutorials.md)

