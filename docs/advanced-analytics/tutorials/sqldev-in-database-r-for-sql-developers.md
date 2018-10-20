---
title: 教程，了解数据库内分析使用 R 和 SQL Server 机器学习 |Microsoft Docs
description: 本教程演示如何在 SQL Server 中嵌入 R 存储过程和 T-SQL 函数
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 651e529bf0aa4cd4b4fab7e292e570dbb78e89d5
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461883"
---
# <a name="tutorial-learn-in-database-analytics-using-r-in-sql-server"></a>教程： 了解在 SQL Server 中使用 R 的数据库内分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本教程中的 SQL 编程人员，可以使用 R 语言构建和部署机器学习的 R 代码包装在存储过程中的解决方案的实践经验。

本教程使用已知的公共数据集，基于在纽约市出租车行程。 若要使示例代码更快地运行，我们创建了具有代表性的 1%抽样数据。 您将使用此数据生成预测特定行程是否可能获得小费或不是，基于如时间、 距离和上车位置的列的二元分类模型。

> [!NOTE]
> 
> 在 Python 中提供了相同的解决方案。 SQL Server 2017 是必需的。 请参阅[-数据库内分析面向 Python 开发人员](../tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="overview"></a>概述

通常构建端到端解决方案的过程包括获取并清洗数据、 数据浏览和特征工程、 模型训练和优化和最后在生产环境中的模型的部署。 是最好使用专门的开发环境执行的实际代码的开发和测试。 对于 R，这可能意味着 RStudio 或[!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]。

但是，在创建该解决方案后，可以在熟悉的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 环境中使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程将其轻松部署到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。

- [NYC 出租车数据库设置](demo-data-nyctaxi-in-sql.md)

- [第 1 课： 浏览和可视化通过存储过程中调用 R 函数的数据形状和分发](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [第 2 课： 创建数据功能在 T-SQL 函数中使用 R](sqldev-create-data-features-using-t-sql.md)
  
- [第 3 课： 训练和保存使用函数和存储的过程的 R 模型](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [第 4 课： 在存储过程中的操作化的包装 R 代码](../tutorials/sqldev-operationalize-the-model.md)。 
  将模型保存到数据库后，使用存储过程从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调用该模型用于预测。

## <a name="prerequisites"></a>必要條件

本教程假定你熟悉基本数据库操作，例如创建数据库和表、 导入数据，以及编写 SQL 查询。 它不会假定您知道。在这种情况下，提供所有 R 代码。 经验丰富的 SQL 编程人员可以使用提供的 PowerShell 脚本，GitHub 上的示例数据并[!INCLUDE[tsql](../../includes/tsql-md.md)]在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]要完成本示例。 

教程： 开始前

- 验证是否有已配置的实例[SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation)或[使用启用了 R 的 SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md#verify-installation)。 此外，[确认你拥有的 R 库](../r/determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location)。
- 本教程中使用的登录名必须有权创建数据库和其他对象，若要上传数据，选择数据，并运行存储的过程。

> [!NOTE]
> 我们建议您不要**不**使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]来编写或测试 R 代码。 如果在存储过程中嵌入的代码有任何问题，从存储过程返回的信息通常不足以了解错误的原因。
> 
> 对于调试，我们建议你使用工具例如[!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]，或 RStudio。 本教程中提供的 R 脚本已使用传统的 R 工具进行开发和调试。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [NYC 出租车数据库设置](demo-data-nyctaxi-in-sql.md)