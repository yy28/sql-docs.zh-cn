---
title: "数据库中 Python 分析 SQL 开发人员 |Microsoft 文档"
ms.custom: 
ms.date: 10/13/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: dab1a9648865f13d1741917bd389eae287afd7f2
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2018
---
# <a name="in-database-python-analytics-for-sql-developers"></a>SQL 开发人员的数据库中 Python 分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

此演练的目的是 SQL 程序员提供生成机器学习解决方案使用在 SQL Server 中运行的 Python 的实践经验。 在本演练中，你将了解如何将 Python 代码添加到存储过程和运行存储的过程生成并从模型预测。

> [!NOTE]
> 更喜欢 R？ 请参阅[本教程](sqldev-in-database-r-for-sql-developers.md)，可提供类似的解决方案，但使用 R，并且可以在 SQL Server 2016 或 SQL Server 自 2017 年中运行。

## <a name="overview"></a>概述

生成机器学习解决方案的过程是一个可以跨多个阶段中涉及多个工具和协调个行业专家的复杂：

+ 获取和清除数据
+ 浏览数据和构建适用于建模的功能
+ 定型集和优化模型
+ 部署到生产环境

**本演练的重点是构建和部署使用 SQL Server 的解决方案。**

数据是来自已知 NYC Taxi 数据集。 若要快速而方便地使本演练中，对数据进行采样。 你将创建用于预测特定行程是否有可能收到一条提示，或不是，基于例如天、 距离和提取位置的时间的列的二元分类模型。

可以完成所有任务使用[!INCLUDE[tsql](../../includes/tsql-md.md)]的熟悉的环境中的存储过程 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]

- [步骤 1：下载示例数据](sqldev-py1-download-the-sample-data.md)

    将示例数据集和所有脚本文件下载到本地计算机。

- [步骤 2：使用 PowerShell 将数据导入 SQL Server](sqldev-py2-import-data-to-sql-server-using-powershell.md)

    执行 PowerShell 脚本的指定实例上创建一个数据库和表并加载到表的示例数据。

- [步骤 3： 浏览和可视化数据使用 Python](sqldev-py3-explore-and-visualize-the-data.md)

    执行基本的数据浏览和可视化效果，通过从调用 Python[!INCLUDE[tsql](../../includes/tsql-md.md)]存储过程。

- [步骤 4： 创建在 T-SQL 中使用 Python 数据功能](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    使用自定义 SQL 函数创建新数据特征。
  
- [步骤 5： 训练和保存 Python 模型使用 T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    生成并保存在存储过程中使用 Python 机器学习模型。
  
    本演练演示如何执行二元分类任务;你也无法使用数据生成的回归或多类分类模型。

  
-  [步骤 6： 具有可操作性 Python 模型](sqldev-py6-operationalize-the-model.md)

    模型已保存到数据库后，调用模型预测使用[!INCLUDE[tsql](../../includes/tsql-md.md)]。

## <a name="requirements"></a>需求

### <a name="prerequisites"></a>必要條件

+ 使用机器学习服务和启用的 Python 安装 SQL Server 2017 的实例。 有关详细信息，请参阅[安装 SQL Server 自 2017 年 1 机器学习 Services （数据库）](../install/sql-machine-learning-services-windows-install.md)。
+ 本演练中使用的登录名必须有权创建数据库和其他对象，有权上载数据、选择数据和运行存储过程。

### <a name="experience-level"></a>体验级别

你应熟悉基本数据库操作，如创建数据库和表、 将数据导入表，以及创建 SQL 查询。

有经验的 SQL 编程人员可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或运行提供的 PowerShell 脚本完成本演练。

Python： 基本知识很有用但并不是必需。 提供的所有 Python 代码。

PowerShell 一些知识将会很有帮助。

### <a name="tools"></a>工具

对于本教程，我们假定你已达到部署阶段。 你有权清理数据，完成功能工程，并使用 Python 代码的 T-SQL 代码。 因此，你可以完成本教程中使用 SQL Server Management Studio 或支持正在运行的 SQL 语句的任何其他工具。

+ [SQL Server 工具的概述](https://docs.microsoft.com/sql/tools/overview-sql-tools) 

如果你想要进行开发和测试你自己的 Python 代码，调试 Python 解决方案，我们建议使用专用的开发环境：

+ **Visual Studio 2017**支持这两个 R 和[Python](https://blogs.msdn.microsoft.com/visualstudio/2017/05/12/a-lap-around-python-in-visual-studio-2017/)。 我们建议[数据科学工作负荷](https://blogs.msdn.microsoft.com/visualstudio/2016/11/18/data-science-workloads-in-visual-studio-2017-rc/)，它还支持 R 和 F #。
+ 如果你有 Visual Studio 的早期版本[Visual Studio 的 Python 扩展](https://docs.microsoft.com/visualstudio/python/python-in-visual-studio)可以轻松地管理多个 Python 环境。
+ PyCharm 是 Python 开发人员的常用 IDE。

    > [!NOTE]
    > 通常情况下，应避免编写或测试新的 Python 代码中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 如果在存储过程中嵌入的代码没有任何问题，则从存储过程返回的信息是通常不足以了解错误的原因。

使用以下资源来帮助你规划和执行成功机器学习项目：

+ [团队数据科学过程](https://docs.microsoft.com/azure/machine-learning/team-data-science-process/overview)

### <a name="estimated-time-required"></a>所需的估计的时间

|步骤| 时间 （小时数）|
|----|----|
|下载示例数据| 0:15|
|将数据导入到 SQL Server 使用 PowerShell|0:15|
|浏览和可视化数据|0:20|
|创建使用 T-SQL 的数据功能|0:30|
|训练和保存模型使用 T-SQL|0:15|
|实施该模型|0:40|

## <a name="get-started"></a>要开始

  [步骤 1：下载示例数据](sqldev-py1-download-the-sample-data.md)
