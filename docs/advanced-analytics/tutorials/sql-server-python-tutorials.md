---
title: SQL Server Python 教程 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c99e5605dad537fddef20fbd091a61cc4e711471
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
ms.locfileid: "31201939"
---
# <a name="sql-server-python-tutorials"></a>SQL Server Python 教程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

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

   本课程演示如何运行代码从远程 Python 终端，使用 SQL Server 计算上下文。 你应该熟悉某种程度上 Python tools 和环境。 示例代码是提供用于创建模型使用**rxLinMod**，从新建**revoscalepy**库。 

+ [SQL 开发人员的数据库中 Python 分析](sqldev-in-database-python-for-sql-developers.md)

    本端到端演练演示了生成使用 T-SQL 存储过程的完整 Python 解决方案的过程。 包含所有 Python 代码都。


## <a name="python-samples"></a>Python 示例

这些示例和演示 SQL Server 开发团队提供的突出显示实际的应用程序中使用嵌入的分析的方式。

+ [构建预测模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  了解如何 ski 租赁业务可能使用机器学习来预测将来出租，它可帮助企业版计划和员工，以满足将来需求。

  > [!TIP]
  > 现在包括从 Python 模型的本机评分 ！

+ [执行客户群集使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    了解如何使用 Kmeans 算法来执行无人监督聚类分析的客户。

## <a name="bkmk_Prerequisites"></a>先决条件

若要使用这些教程，你必须具有 SQL Server 自 2017 年 1，并且你必须显式安装，然后启用的功能，机器学习服务 （数据库）。 

SQL Server 2017 支持 R 和 Python 的语言，但既不是安装或启用默认情况下。 运行 Python 需要启用扩展性框架，并且必须为要安装的语言选择 Python。 

### <a name="post-installation-configuration-tips"></a>安装后配置提示

运行 SQL Server 安装程序之后, 你可能需要执行一些附加步骤以确保 Python 和 SQL Server 进行通信：

+ 通过运行启用外部脚本执行功能`sp_configure 'external scripts enabled', 1`。
+ 重新启动服务器。 
+ 打开**服务**面板，以检查是否已启动快速启动板。 
+ 确保调用外部运行时的服务具有必要权限。 有关详细信息，请参阅[默示身份验证的启用](../r/add-sqlrusergroup-to-database.md)。
+ 对于 SQL Server，打开防火墙上的端口，并启用所需的网络协议。
+ 确保你的 SQL 登录名或 Windows 用户帐户具有连接到服务器，以读取数据，并创建此示例要求任何数据库对象所必需的权限。

请参阅此文章有关的一些常见问题：[疑难解答机器学习服务](../machine-learning-troubleshooting-faq.md)

### <a name="resource-management"></a>资源管理

你可以在同一台计算机上安装 R 和 Python，但运行可能需要大量资源。 如果你遇到"内存不足"错误，或者如果正在运行的机器学习作业是主体服务器的用途，你可以减少分配给数据库引擎的内存量。 有关详细信息，请参阅[管理和监视 SQL Server 中的 Python](../python/managing-and-monitoring-python-solutions.md)。

## <a name="see-also"></a>另请参阅

[SQL Server 的 R 教程](sql-server-r-tutorials.md)
