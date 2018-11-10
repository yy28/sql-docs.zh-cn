---
title: 教程，了解数据库内分析使用 R 和 SQL Server 机器学习 |Microsoft Docs
description: 了解如何将嵌入 R 编程语言在 SQL Server 存储过程和 T-SQL 函数中的代码。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 80c4d39e87984b022340079be4d944ed6ad963e3
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "51030644"
---
# <a name="tutorial-in-database-r-analytics-for-sql-developers"></a>教程： SQL 开发人员的数据库内 R 分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在为 SQL 程序员提供本教程中，了解有关 R 集成的生成和部署的基于 R 的机器学习解决方案： 使用[NYCTaxi_sample](demo-data-nyctaxi-in-sql.md)上 SQL Server 数据库。 

本教程向您介绍一种数据建模工作流中使用的 R 函数。 步骤包括数据探索、 构建和训练二元分类模型和模型部署。 将使用从 New York City Taxi 和 Limosine 委员会的示例数据并将生成的模型预测某个行程是否可能会导致基于时间、 上移动，距离和上车位置的提示。 在本教程中使用的 R 代码的所有包装在存储过程创建并在 Management Studio 中运行。


> [!NOTE]
> 
> 本教程是在 R 和 Python 中可用。 Python 版本，请参阅[-数据库内分析面向 Python 开发人员](../tutorials/sqldev-in-database-python-for-sql-developers.md)。

## <a name="overview"></a>概述

构建机器学习解决方案的过程很复杂，可以跨多个阶段中涉及多个工具和协调的主题事项专家：

+ 获取并清洗数据
+ 浏览数据和构建适用于建模的功能，
+ 定型集和优化模型
+ 部署到生产环境

是最好使用专门的开发环境执行的实际代码的开发和测试。 但是，在全面测试该脚本后，你可以轻松地将其部署到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用[!INCLUDE[tsql](../../includes/tsql-md.md)]的熟悉的环境中的存储过程[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。

是否是 SQL 程序员不熟悉 R，或者是否熟悉 SQL，此多部分教程的 R 开发人员引入了执行使用 R 和 SQL Server 数据库内分析的典型工作流。 

- [第 1 课： 浏览和可视化通过存储过程中调用 R 函数的数据形状和分发](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [第 2 课： 创建数据功能在 T-SQL 函数中使用 R](sqldev-create-data-features-using-t-sql.md)
  
- [第 3 课： 训练和保存使用函数和存储的过程的 R 模型](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [第 4 课： 预测潜在的存储过程中使用 R 模型的结果](../tutorials/sqldev-operationalize-the-model.md)

该模型保存到数据库后，调用该模型用于预测[!INCLUDE[tsql](../../includes/tsql-md.md)]通过使用存储的过程。

## <a name="prerequisites"></a>必要條件

可以完成所有任务使用[!INCLUDE[tsql](../../includes/tsql-md.md)]中的存储过程[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。

本教程假定你熟悉基本数据库操作，例如创建数据库和表、 导入数据，以及编写 SQL 查询。 它不会假定您知道。在这种情况下，提供所有 R 代码。 

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation)或[使用启用了 R 的 SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [R 库](../r/determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location)

+ [权限](../security/user-permission.md)

+ [NYC 出租车演示数据库](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [NYC 出租车数据库设置](demo-data-nyctaxi-in-sql.md)