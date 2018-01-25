---
title: "SQL Server Python 教程 |Microsoft 文档"
ms.custom: SQL2016_New_Updated
ms.date: 09/19/2017
vapplies_to: SQL Server 2017
dev_langs: Python
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 7fc78e8055e72066925b1c9dee8534aea681933c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="sql-server-python-tutorials"></a>SQL Server Python 教程

本文提供教程和示例演示如何使用 Python 与 SQL Server 2017 的列表。 通过这些示例和演示，你将学习：

+ 如何从 T-SQL 运行 Python
+ 远程和本地计算上下文和如何可以执行 Python 代码中使用 SQL Server 计算机有哪些？
+ 如何将 Python 代码包装在存储过程
+ 优化 SQL 生产环境中的 Python 代码
+ 为应用程序中嵌入机器学习的实际方案

有关要求和安装程序的信息，请参阅[先决条件](#bkmk_Prerequisites)。

## <a name="bkmk_pythontutorials"></a>Python 教程

+ [在 T-SQL 中运行 Python](run-python-using-t-sql.md)

   了解如何在 T-SQL 中使用率先推出了在 SQL Server 2016 中的扩展性机制中调用 Python 的基础知识。

+ [创建机器学习中使用 revoscalepy Python 模型](use-python-revoscalepy-to-create-model.md)

   你将创建模型使用**rxLinMod**，从新建**revoscalepy**库。 将启动远程 Python 终端中的代码，但建模，会在 SQL Server 计算上下文中的进行。

+ [SQL 开发人员的数据库中 Python 分析](sqldev-in-database-python-for-sql-developers.md)

  新！ 生成使用 T-SQL 存储过程的完整 Python 解决方案。 包含所有 Python 代码都。

+ [部署和使用 Python 模型](..\python\publish-consume-python-code.md)

  了解如何部署使用 Microsoft 机器学习 Server 的最新版本的 Python 模型。

## <a name="python-samples"></a>Python 示例

这些示例和演示 SQL Server 开发团队提供的突出显示实际的应用程序中使用嵌入的分析的方式。

+ [构建预测模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  了解如何 ski 租赁业务可能使用机器学习来预测将来出租，它可帮助企业版计划和员工，以满足将来需求。

  > [!TIP]
  > 现在包括从 Python 模型的本机评分 ！

+ [执行客户群集使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    了解如何使用 Kmeans 算法来执行无人监督聚类分析的客户。

## <a name="bkmk_Prerequisites"></a>先决条件

若要使用这些教程，你必须已安装 SQL Server 自 2017 年 1 机器学习 Services （数据库）。 SQL Server 2017 支持 R 或 Python。 但是，你必须安装扩展性框架，支持机器学习中，并选择 Python 作为要安装的语言。 你可以在同一台计算机上安装 R 和 Python。

> [!NOTE]
>
> 对于 Python 支持是 SQL Server 自 2017 年中的新功能，并需要 CTP 2.0 或更高版本。 尽管该功能是预发行版和不受支持生产环境中，但我们邀请您能够对其进行测试和发送反馈。

**SQL Server 2017**

运行 SQL Server 安装程序之后, 不要忘记以下重要步骤：

+ 通过运行启用外部脚本执行功能`sp_configure 'external scripts enabled', 1`。
+ 重新启动服务器。
+ 确保调用外部运行时的服务具有必要权限。
+ 确保你的 SQL 登录名或 Windows 用户帐户具有连接到服务器，以读取数据，并创建此示例要求任何数据库对象所必需的权限。

如果你遇到问题，请参阅此文章了解遇到的一些常见问题：[疑难解答机器学习服务](../machine-learning-troubleshooting-faq.md)

## <a name="see-also"></a>另请参阅

[SQL Server 的 R 教程](sql-server-r-tutorials.md)
