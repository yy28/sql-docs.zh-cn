---
title: 中的数据库 Python 分析面向 SQL 开发人员 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 250d2efd6d212348083f5dc3bbc355c466f4811b
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461853"
---
# <a name="in-database-python-analytics-for-sql-developers"></a>SQL 开发人员的数据库内 Python 分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本演练的目的是向 SQL 程序员介绍构建的机器学习使用 Python 在 SQL Server 中运行的解决方案的实践经验。 在本演练中，将了解如何将 Python 代码添加到存储过程和运行存储的过程以生成并从模型预测。

> [!NOTE]
> 更喜欢 R？ 请参阅[本教程](sqldev-in-database-r-for-sql-developers.md)，它提供了类似的解决方案，但使用 R，并可以在 SQL Server 2016 或 SQL Server 2017 中运行。

## <a name="overview"></a>概述

构建机器学习解决方案的过程很复杂，可以跨多个阶段中涉及多个工具和协调的主题事项专家：

+ 获取并清洗数据
+ 浏览数据和构建适用于建模的功能，
+ 定型集和优化模型
+ 部署到生产环境

**本演练的重点是构建和部署使用 SQL Server 的解决方案。**

数据是从众所周知的 NYC 出租车数据集。 若要快速而简单，使本演练中，数据进行采样。 将创建预测特定行程是否可能获得小费或不是，基于如时间、 距离和上车位置的列的二元分类模型。

可以完成所有任务使用[!INCLUDE[tsql](../../includes/tsql-md.md)]的熟悉的环境中的存储过程 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]

- [步骤 1：下载示例数据](demo-data-nyctaxi-in-sql.md)

    将示例数据集和所有脚本文件下载到本地计算机。

- [步骤 2：使用 PowerShell 将数据导入 SQL Server](sqldev-py2-import-data-to-sql-server-using-powershell.md)

    执行的指定实例上创建一个数据库和表并加载示例数据到表的 PowerShell 脚本。

- [步骤 3： 浏览和使用 Python 将数据可视化](sqldev-py3-explore-and-visualize-the-data.md)

    执行基本的数据浏览和可视化，通过调用 Python 的[!INCLUDE[tsql](../../includes/tsql-md.md)]存储过程。

- [步骤 4： 创建数据功能在 T-SQL 中使用 Python](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    使用自定义 SQL 函数创建新数据特征。
  
- [步骤 5： 训练和保存使用 T-SQL 的 Python 模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    生成并保存机器学习模型，在存储过程中使用 Python。
  
    本演练演示如何执行二进制分类任务;此外可以使用数据来生成用于回归还是多类分类模型。

  
-  [步骤 6： 操作 Python 模型](sqldev-py6-operationalize-the-model.md)

    该模型保存到数据库后，调用该模型用于预测使用[!INCLUDE[tsql](../../includes/tsql-md.md)]。

## <a name="requirements"></a>要求

### <a name="prerequisites"></a>必要條件

+ 使用机器学习服务和启用的 Python 安装 SQL Server 2017 的实例。 有关详细信息，请参阅[安装 SQL Server 2017 机器学习服务 （数据库内）](../install/sql-machine-learning-services-windows-install.md)。
+ 本演练中使用的登录名必须有权创建数据库和其他对象，有权上载数据、选择数据和运行存储过程。

### <a name="experience-level"></a>体验级别

您应熟悉基本数据库操作，如创建数据库和表、 数据导入表，以及创建 SQL 查询。

有经验的 SQL 编程人员可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或运行提供的 PowerShell 脚本完成本演练。

Python： 基础知识是非常有用，但并不是必需。 提供了所有 Python 代码。

PowerShell 的一些知识很有帮助。

### <a name="tools"></a>工具

对于本教程中，我们假定你已达到部署阶段。 拥有清理数据、 完整的功能工程，并使用 Python 代码的 T-SQL 代码。 因此，可以完成本教程中使用 SQL Server Management Studio 或支持运行 SQL 语句的任何其他工具。

+ [SQL Server 工具的概述](https://docs.microsoft.com/sql/tools/overview-sql-tools) 

如果想要开发和测试您自己的 Python 代码，或调试 Python 解决方案，我们建议使用专用的开发环境：

+ **Visual Studio 2017**支持这两个 R 和[Python](https://blogs.msdn.microsoft.com/visualstudio/2017/05/12/a-lap-around-python-in-visual-studio-2017/)。 我们建议[数据科学工作负荷](https://blogs.msdn.microsoft.com/visualstudio/2016/11/18/data-science-workloads-in-visual-studio-2017-rc/)，它还支持 R 和 F #。
+ 如果您具有早期版本的 Visual Studio 中， [Visual Studio 的 Python 扩展](https://docs.microsoft.com/visualstudio/python/python-in-visual-studio)轻松地管理多个 Python 环境。
+ PyCharm 是在 Python 开发人员之间的热门 IDE。

    > [!NOTE]
    > 通常情况下，应避免编写或测试中的新 Python 代码[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 如果在存储过程中嵌入的代码有任何问题，从存储过程返回的信息通常不足以了解错误的原因。

使用以下资源可帮助您规划和执行成功的机器学习项目：

+ [团队数据科学过程](https://docs.microsoft.com/azure/machine-learning/team-data-science-process/overview)

### <a name="estimated-time-required"></a>所需的估计的时间

|步骤| 时间 （小时数）|
|----|----|
|下载示例数据| 0:15|
|数据导入到 SQL Server 使用 PowerShell|0:15|
|浏览和可视化数据|0:20|
|使用 T-SQL 创建数据功能|0:30|
|训练和保存使用 T-SQL 的模型|0:15|
|运营模型|0:40|

## <a name="get-started"></a>入门

  [步骤 1：下载示例数据](demo-data-nyctaxi-in-sql.md)
