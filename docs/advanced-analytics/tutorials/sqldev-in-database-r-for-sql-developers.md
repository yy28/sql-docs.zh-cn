---
title: 使用 R 进行数据库内分析的教程
description: 了解如何在 SQL Server 存储过程和 T-sql 函数中嵌入 R 编程语言代码。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1257cc3f3d0b3ed07bc879f5bc3337d62bc1b3a0
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470573"
---
# <a name="tutorial-r-data-analytics-for-sql-developers"></a>教程：适用于 SQL 开发人员的 R 数据分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本教程中, 针对 SQL 程序员, 通过使用 SQL Server 上的[NYCTaxi_sample](demo-data-nyctaxi-in-sql.md)数据库生成和部署基于 r 的机器学习解决方案来了解 r 集成。 你将使用 T-sql、SQL Server Management Studio 和数据库引擎实例, 其中包含 [机器学习服务] ([机器学习服务](../install/sql-machine-learning-services-windows-install.md)和 R 语言支持

本教程介绍数据建模工作流中使用的 R 函数。 步骤包括数据浏览、构建和培训二元分类模型和模型部署。 要生成的模型将预测行程是否可能会根据一天中的时间、距离和取货位置导致提示。 

本教程中使用的所有 R 代码包装在 Management Studio 中创建和运行的存储过程中。

## <a name="background-for-sql-developers"></a>面向 SQL 开发人员的背景

构建机器学习解决方案的过程是一项复杂的工作, 它可以涉及多个工具, 并跨多个阶段协调主题专家:

+ 获取和清理数据
+ 探索用于建模的数据和生成功能
+ 训练和优化模型
+ 部署到生产

最佳做法是使用专用的 R 开发环境来执行实际代码的开发和测试。 但是, 在对脚本进行完全测试后, 你可以轻松地将[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]其[!INCLUDE[tsql](../../includes/tsql-md.md)]部署到[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]在熟悉的环境中使用存储过程。

此多部分教程的目的是介绍将 "已完成的 R 代码" 迁移到 SQL Server 的典型工作流。 

- [第 1 课：通过在存储过程中调用 R 函数来浏览和可视化数据形状和分布](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [第 2 课：在 T-sql 函数中使用 R 创建数据功能](sqldev-create-data-features-using-t-sql.md)
  
- [第 3 课：使用函数和存储过程定型并保存 R 模型](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [第 4 课：在存储过程中使用 R 模型预测潜在结果](../tutorials/sqldev-operationalize-the-model.md)

在将模型保存到数据库后, [!INCLUDE[tsql](../../includes/tsql-md.md)]通过使用存储过程调用模型以获取预测。

## <a name="prerequisites"></a>先决条件

所有任务都可以使用[!INCLUDE[tsql](../../includes/tsql-md.md)]中的[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]存储过程完成。

本教程假定你熟悉基本数据库操作, 例如创建数据库和表、导入数据以及编写 SQL 查询。 它不会假设你知道 R。因此, 提供了所有 R 代码。 

+ [SQL Server 2016 r Services](../install/sql-r-services-windows-install.md#verify-installation)或[SQL Server 2017 机器学习服务启用 r](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [R 库](../package-management/installed-package-information.md)

+ [权限](../security/user-permission.md)

+ [NYC 出租车演示数据库](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用存储过程中的 R 函数浏览和可视化数据](../tutorials/sqldev-explore-and-visualize-the-data.md)
