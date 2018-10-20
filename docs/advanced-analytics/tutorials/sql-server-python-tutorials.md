---
title: SQL Server Python 教程 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 5cafb253cea118148bd654ea770234843f742838
ms.sourcegitcommit: b1990ec4491b5a8097c3675334009cb2876673ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2018
ms.locfileid: "49383332"
---
# <a name="sql-server-python-tutorials"></a>SQL Server Python 教程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供了一系列教程和示例演示了如何使用 Python 与 SQL Server 2017。 通过这些示例和演示，你将了解：

+ 如何从 T-SQL 运行 Python
+ 远程和本地计算上下文和如何执行 Python 代码中使用 SQL Server 计算机是什么
+ 如何在存储过程中包装 Python 代码
+ 优化 SQL 生产环境中的 Python 代码
+ 用于在应用程序中嵌入机器学习的实际方案

有关要求和安装程序的信息，请参阅[先决条件](#bkmk_Prerequisites)。

## <a name="bkmk_pythontutorials"></a>Python 教程

+ [在 T-SQL 中运行 Python](run-python-using-t-sql.md)

   了解如何在 T-SQL，使用 SQL Server 2016 中率先采用的扩展性机制调用 Python 的基础知识。

+ [创建机器学习中使用 revoscalepy Python 模型](use-python-revoscalepy-to-create-model.md)

   本课程演示如何运行代码从远程 Python 终端，使用 SQL Server 计算上下文。 应为一定程度上熟悉的 Python 工具和环境。 提供用于创建模型使用的示例代码， **rxLinMod**，从新建**revoscalepy**库。 

+ [SQL 开发人员的数据库内 Python 分析](sqldev-in-database-python-for-sql-developers.md)

    本端到端演练演示如何构建完整的 Python 解决方案使用 T-SQL 存储过程的过程。 包含所有 Python 代码都。


## <a name="python-samples"></a>Python 示例

这些示例和演示 SQL Server 开发团队提供的突出显示您可以在实际应用程序中使用嵌入式的分析方法。

+ [构建预测模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  介绍了雪橇租赁公司如何使用机器学习来预测未来的租赁情况，可帮助业务和人员计划以满足未来的需求。

  > [!TIP]
  > 现在包括本机计分从 Python 模型 ！

+ [执行客户使用 Python 和 SQL Server 聚类分析](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    了解如何使用 k 均值算法执行无人监督聚类分析的客户。

## <a name="see-also"></a>请参阅

[SQL Server 的 R 教程](sql-server-r-tutorials.md)
