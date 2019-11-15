---
title: Python + T-SQL：开发模型
description: 了解如何在 SQL Server 存储过程和 T-SQL 函数中嵌入 Python 代码。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b67be59da71667167594ef82e67dfef6f8118fbb
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "73725219"
---
# <a name="tutorial-python-data-analytics-for-sql-developers"></a>教程：适用于 SQL 开发者的 Python 数据分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在面向 SQL 程序员的本教程中，使用 SQL Server 上的 [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) 数据库来构建和部署基于 Python 的机器学习解决方案，以了解 Python 集成。 你将使用 T-SQL、SQL Server Management Studio 和数据库引擎实例，其中包含[机器学习服务](../install/sql-machine-learning-services-windows-install.md)和 Python 语言支持。

本教程介绍在数据建模工作流中使用的 Python 函数。 这包括数据浏览、构建和定型二元分类模型以及模型部署等步骤。 你将使用来自纽约市出租车和轿车管理委员会的示例数据，将建立的模型根据一天中的时间、行进的距离和接送地点来预测出行是否会给小费。 

本教程中使用的所有 Python 代码都包装在你在 Management Studio 中创建并运行的存储过程中。

> [!NOTE]
> R 和 Python 均提供此教程。 对于 R 版本，请参阅[适用于 R 开发人员的数据库内分析](sqldev-in-database-r-for-sql-developers.md)。

## <a name="overview"></a>概述

构建机器学习解决方案是一种复杂的过程，它可能涉及多种工具，并且需要主题专家跨多个阶段进行协调：

+ 获取和清除数据
+ 探索数据并构建有助于建模的功能
+ 定型和优化模型
+ 部署到生产环境

使用专用的开发环境，可以以最佳方式执行实际代码的开发和测试。 但是，在完全测试该脚本后，可以在熟悉的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 环境中使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程将其轻松部署到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在存储过程中包装外部代码是在 SQL Server 中操作代码的主要机制。

无论你是不熟悉 Python 的 SQL 程序员，还是不熟悉 SQL 的 Python 开发人员，都可借助本系列教程，了解使用 Python 和 SQL Server 进行数据库内分析的典型工作流程。 

+ [第 1 课：使用 Python 浏览并可视化数据](sqldev-py3-explore-and-visualize-the-data.md)

+ [第 2 课：使用自定义 SQL 函数创建数据特征](sqldev-py4-create-data-features-using-t-sql.md)

+ [第 3 课：使用 T-SQL 定型和保存 Python 模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

+ [第 4 课：在存储过程中使用 Python 模型预测潜在结果](sqldev-py6-operationalize-the-model.md)

将模型保存到数据库后，可以使用存储过程从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调用该模型以用于预测。

## <a name="prerequisites"></a>必备条件

+ [使用 Python 的 SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [权限](../security/user-permission.md)

+ [纽约市出租车演示数据库](demo-data-nyctaxi-in-sql.md)

所有任务都可以使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程来完成。

本教程假定你熟悉基本数据库操作，例如创建数据库和表、导入数据以及编写 SQL 查询。 它不假设你了解 Python。 因此，提供了所有 Python 代码。 

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 Python 浏览并可视化数据](sqldev-py3-explore-and-visualize-the-data.md)
