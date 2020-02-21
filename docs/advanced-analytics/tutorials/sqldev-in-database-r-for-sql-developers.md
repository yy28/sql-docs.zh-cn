---
title: R + T-SQL 教程：开发模型
description: 了解如何在 SQL Server 存储过程和 T-SQL 函数中嵌入 R 编程语言代码。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9669b2c38d2e8b571ef7e519100b13cf5a63a10d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "74479413"
---
# <a name="tutorial-r-data-analytics-for-sql-developers"></a>教程：适用于 SQL 开发者的 R 数据分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在面向 SQL 程序员的本教程中，使用 SQL Server 上的 [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) 数据库来构建和部署基于 R 的机器学习解决方案，以了解 R 集成。 你将使用 T-SQL、SQL Server Management Studio 和数据库引擎实例，其中包含[机器学习服务](../install/sql-machine-learning-services-windows-install.md)和 R 语言支持

本教程介绍在数据建模工作流中使用的 R 函数。 这包括数据浏览、构建和定型二元分类模型以及模型部署等步骤。 要构建的模型会根据一天中的时间、行程距离和上车位置预测行程是否可能产生小费。 

本教程中使用的所有 R 代码都包装在你在 Management Studio 中创建并运行的存储过程中。

## <a name="background-for-sql-developers"></a>SQL 开发者背景

构建机器学习解决方案是一种复杂的过程，它可能涉及多种工具，并且需要主题专家跨多个阶段进行协调：

+ 获取和清除数据
+ 探索数据并构建有助于建模的功能
+ 定型和优化模型
+ 部署到生产环境

实际代码的开发和测试最好使用专用的 R 开发环境进行。 但是，在完全测试该脚本后，可以在熟悉的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 环境中使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程将其轻松部署到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

此多部分教程的目的是介绍将“已完成的 R 代码”迁移到 SQL Server 的典型工作流。 

- [第 1 课：通过在存储过程中调用 R 函数来探索和可视化数据的形态和分布](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [第 2 课：在 T-SQL 函数中使用 R 来创建数据特征](sqldev-create-data-features-using-t-sql.md)
  
- [第 3 课：使用函数和存储过程定型并保存 R 模型](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [第 4 课：在存储过程中使用 R 模型预测潜在结果](../tutorials/sqldev-operationalize-the-model.md)

将模型保存到数据库后，使用存储过程从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调用该模型以用于预测。

## <a name="prerequisites"></a>必备条件

所有任务都可以使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程来完成。

本教程假定你熟悉基本数据库操作，例如创建数据库和表、导入数据以及编写 SQL 查询。 但并未要求你了解 R。因此，本教程提供了所有 R 代码。 

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation) 或[已启用 R 的 SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [R 库](../package-management/r-package-information.md)

+ [权限](../security/user-permission.md)

+ [纽约市出租车演示数据库](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [在存储过程中使用 R 函数探索和可视化数据](../tutorials/sqldev-explore-and-visualize-the-data.md)
