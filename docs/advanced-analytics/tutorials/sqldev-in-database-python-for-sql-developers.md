---
title: "数据库中 Python 分析 SQL 开发人员 |Microsoft 文档"
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 984ff8097b1f28cf11e28cc464c88dc3b9580a12
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="in-database-python-analytics-for-sql-developers"></a>数据库中 Python 分析 SQL 开发人员

此演练的目的是 SQL 程序员提供生成机器学习在 SQL Server 中的解决方案的实践经验。 在本演练中，你将了解如何通过将 Python 代码添加到存储过程中将 Python 合并到应用程序。

> [!NOTE]
> 更喜欢 R？ 请参阅[本教程](sqldev-in-database-r-for-sql-developers.md)、 它提供类似的解决方案，但使用 R，和可以在 SQL Server 2016 或 SQL Server 2017 eb 运行。

## <a name="overview"></a>概述

构建端到端解决方案的过程通常包括获取并清洗数据、数据探索和功能研发、模型训练和调优，以及最后在生产中部署模型。 开发和测试的实际代码的最佳执行使用的专用的开发环境，例如这些 Python 工具：

+ PyCharm，常用的 IDE
+ Spyder，它又包括在[Visual Studio 2017](https://blogs.msdn.microsoft.com/visualstudio/2017/05/12/a-lap-around-python-in-visual-studio-2017/)如果你安装[数据科学工作负荷](https://blogs.msdn.microsoft.com/visualstudio/2016/11/18/data-science-workloads-in-visual-studio-2017-rc/)
+ [Visual Studio 的 Python 扩展](https://docs.microsoft.com/visualstudio/python/python-in-visual-studio)。

创建并在 IDE 中测试解决方案后，你可以部署到的 Python 代码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用[!INCLUDE[tsql](../../includes/tsql-md.md)]的熟悉的环境中的存储过程[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。

在本演练中，我们将假定为您提供了该解决方案所需的所有 Python 代码和你重点介绍如何构建和部署使用 SQL Server 的解决方案。

- [步骤 1：下载示例数据](sqldev-py1-download-the-sample-data.md)

  将示例数据集和所有脚本文件下载到本地计算机。

- [步骤 2：使用 PowerShell 将数据导入 SQL Server](sqldev-py2-import-data-to-sql-server-using-powershell.md)

  执行 PowerShell 脚本的指定实例上创建一个数据库和表并加载到表的示例数据。

- [步骤 3：浏览和可视化数据](sqldev-py3-explore-and-visualize-the-data.md)

  执行基本的数据浏览和可视化效果，通过从调用 Python[!INCLUDE[tsql](../../includes/tsql-md.md)]存储过程。

- [步骤 4：使用 T-SQL 创建数据功能](sqldev-py5-train-and-save-a-model-using-t-sql.md)

  使用自定义 SQL 函数创建新数据特征。
  
- [步骤 5：使用 T-SQL 定型和保存模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

   生成并保存在存储过程中使用 Python 机器学习模型。
  
-  [步骤 6：操作模型](sqldev-py6-operationalize-the-model.md)

  模型已保存到数据库后，调用模型预测使用[!INCLUDE[tsql](../../includes/tsql-md.md)]。

> [!NOTE]
> 我们建议你不要使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]编写或测试 Python 代码。 如果在存储过程中嵌入的代码没有任何问题，则从存储过程返回的信息是通常不足以了解错误的原因。


### <a name="scenario"></a>应用场景

本演练使用众所周知的 NYC Taxi 数据集。 若要快速而方便地使本演练中，对数据进行采样。 使用此数据，你将创建用于预测特定行程是否有可能收到一条提示，或不是，基于例如天、 距离和提取位置的时间的列的二元分类模型。

### <a name="requirements"></a>要求

本演练面向已熟悉基本数据库操作的用户，如创建数据库和表、将数据导入表，以及创建 SQL 查询。

提供的所有 Python 代码。 有经验的 SQL 编程人员可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或运行提供的 PowerShell 脚本完成本演练。

在开始本演练之前, 必须完成下列准备工作：

- 使用机器学习服务和启用的 Python 安装的 SQL Server 2017 实例 （需要 CTP 2.0 或更高版本）。
- 本演练中使用的登录名必须有权创建数据库和其他对象，有权上载数据、选择数据和运行存储过程。

## <a name="next-step"></a>下一步

  [步骤 1：下载示例数据](sqldev-py1-download-the-sample-data.md)

## <a name="see-also"></a>另请参阅

[机器学习服务与 Python](../python/sql-server-python-services.md)



