---
title: 中的数据库 Python 分析面向 SQL 开发人员 |Microsoft Docs
description: 了解如何在 SQL Server 存储过程和 T-SQL 函数中嵌入 Python 代码。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8c992cbda06d158bec0b76d6d46d71157a08cf3e
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "51032984"
---
# <a name="tutorial-in-database-python-analytics-for-sql-developers"></a>教程： SQL 开发人员的数据库内 Python 分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本教程中的 SQL 编程人员，了解有关 Python 集成通过构建和部署基于 Python 的机器学习解决方案： 使用[NYCTaxi_sample](demo-data-nyctaxi-in-sql.md)上 SQL Server 数据库。 

本教程向您介绍一种数据建模工作流中使用的 Python 函数。 步骤包括数据探索、 构建和训练二元分类模型和模型部署。 将使用从 New York City Taxi 和 Limosine 委员会的示例数据并将生成的模型预测某个行程是否可能会导致基于时间、 上移动，距离和上车位置的提示。 在本教程中使用的 Python 代码的所有包装在存储过程创建并在 Management Studio 中运行。

> [!NOTE]
> 本教程是在 R 和 Python 中可用。 对于 R，请参阅[-数据库内分析 R 开发人员](sqldev-in-database-r-for-sql-developers.md)。

## <a name="overview"></a>概述

构建机器学习解决方案的过程很复杂，可以跨多个阶段中涉及多个工具和协调的主题事项专家：

+ 获取并清洗数据
+ 浏览数据和构建适用于建模的功能，
+ 定型集和优化模型
+ 部署到生产环境

是最好使用专门的开发环境执行的实际代码的开发和测试。 但是，在全面测试该脚本后，你可以轻松地将其部署到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用[!INCLUDE[tsql](../../includes/tsql-md.md)]的熟悉的环境中的存储过程[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 将外部代码包装在存储过程中是用于 SQL Server 中的操作代码的主要机制。

无论您是 SQL 程序员熟悉 Python 或 Python 开发人员熟悉 SQL，此多部分教程介绍了执行使用 Python 和 SQL Server 数据库内分析的典型工作流。 

+ [第 1 课： 浏览和可视化使用 Python 的数据](sqldev-py3-explore-and-visualize-the-data.md)

+ [第 2 课： 创建数据功能使用自定义 SQL 函数](sqldev-py4-create-data-features-using-t-sql.md)

+ [第 3 课： 训练和保存使用 T-SQL 的 Python 模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

+ [第 4 课： 预测潜在的结果在存储过程中使用 Python 模型](sqldev-py6-operationalize-the-model.md)

该模型保存到数据库后，您可以调用该模型用于预测[!INCLUDE[tsql](../../includes/tsql-md.md)]通过使用存储的过程。

## <a name="prerequisites"></a>必要條件

+ [与 Python 配合使用的 SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [权限](../security/user-permission.md)

+ [NYC 出租车演示数据库](demo-data-nyctaxi-in-sql.md)

可以完成所有任务使用[!INCLUDE[tsql](../../includes/tsql-md.md)]中的存储过程[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。

本教程假定你熟悉基本数据库操作，例如创建数据库和表、 导入数据，以及编写 SQL 查询。 它不会假设你知道 Python。 在这种情况下，提供了所有 Python 代码。 

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [浏览和可视化使用 Python 的数据](sqldev-py3-explore-and-visualize-the-data.md)
