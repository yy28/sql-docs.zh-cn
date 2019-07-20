---
title: 面向 SQL 开发人员的数据库内 Python 分析教程
description: 了解如何在 SQL Server 存储过程和 T-sql 函数中嵌入 Python 代码。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: ed8008bbda76bfc8a194897e9389c9d5dc6bb031
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345935"
---
# <a name="tutorial-python-data-analytics-for-sql-developers"></a>教程：适用于 SQL 开发人员的 Python 数据分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本教程中, 针对 SQL 程序员, 通过使用 SQL Server 上的[NYCTaxi_sample](demo-data-nyctaxi-in-sql.md)数据库生成和部署基于 python 的机器学习解决方案来了解 python 集成。 你将使用 T-sql、SQL Server Management Studio 和数据库引擎实例, 其中包含[机器学习服务](../install/sql-machine-learning-services-windows-install.md)和 Python 语言支持。

本教程介绍数据建模工作流中使用的 Python 函数。 步骤包括数据浏览、构建和培训二元分类模型和模型部署。 您将使用纽约出租车和 Limosine 委员会的示例数据, 您将生成的模型将预测行程是否可能会根据当天的时间、距离来到另一和拾取位置导致提示。 

本教程中使用的所有 Python 代码包装在 Management Studio 中创建和运行的存储过程中。

> [!NOTE]
> 此教程适用于 R 和 Python。 对于 R 版本, 请参阅[r 开发人员的数据库内分析](sqldev-in-database-r-for-sql-developers.md)。

## <a name="overview"></a>概述

构建机器学习解决方案的过程是一项复杂的工作, 它可以涉及多个工具, 并跨多个阶段协调主题专家:

+ 获取和清理数据
+ 探索用于建模的数据和生成功能
+ 训练和优化模型
+ 部署到生产

最佳做法是使用专用开发环境来执行实际代码的开发和测试。 但是, 在对脚本进行完全测试后, 你可以轻松地将[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]其[!INCLUDE[tsql](../../includes/tsql-md.md)]部署到[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]在熟悉的环境中使用存储过程。 在存储过程中包装外部代码是 SQL Server 中的实现代码的主要机制。

无论你是适用于 Python 的 SQL 程序员, 还是 SQL 的新的 Python 开发人员, 此多部分教程都介绍了使用 Python 和 SQL Server 执行数据库内分析的典型工作流。 

+ [第 1 课：使用 Python 浏览和可视化数据](sqldev-py3-explore-and-visualize-the-data.md)

+ [第 2 课：使用自定义 SQL 函数创建数据功能](sqldev-py4-create-data-features-using-t-sql.md)

+ [第 3 课：使用 T-sql 定型和保存 Python 模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

+ [第 4 课：使用存储过程中的 Python 模型预测潜在结果](sqldev-py6-operationalize-the-model.md)

在将模型保存到数据库后, 您可以[!INCLUDE[tsql](../../includes/tsql-md.md)]通过使用存储过程调用模型以获取预测。

## <a name="prerequisites"></a>先决条件

+ [SQL Server 2017 机器学习服务与 Python](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [权限](../security/user-permission.md)

+ [NYC 出租车演示数据库](demo-data-nyctaxi-in-sql.md)

所有任务都可以使用[!INCLUDE[tsql](../../includes/tsql-md.md)]中的[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]存储过程完成。

本教程假定你熟悉基本数据库操作, 例如创建数据库和表、导入数据以及编写 SQL 查询。 它不会假设你知道 Python。 因此, 提供了所有 Python 代码。 

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 Python 浏览和可视化数据](sqldev-py3-explore-and-visualize-the-data.md)
