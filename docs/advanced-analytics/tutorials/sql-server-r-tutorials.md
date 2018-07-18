---
title: SQL Server R 教程 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e1a6329acbc4d05faa073196b1e5e8d54d78442a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
ms.locfileid: "31202089"
---
# <a name="sql-server-r-tutorials"></a>SQL Server R 教程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供的教程和示例演示与 SQL Server 2016 或 SQL Server 2017 R 的列表。 通过这些示例和演示，你将学习：

+ 如何从 T-SQL 运行 R
+ 什么是远程和本地计算上下文，以及如何执行 R 代码中使用 SQL Server 计算机
+ 如何将 R 代码包装在存储过程
+ 优化 SQL 生产环境中的 R 代码
+ 为应用程序中嵌入机器学习的实际方案

有关要求和安装程序的信息，请参阅[先决条件](#bkmk_Prerequisites)。

## <a name="bkmk_sqltutorials"></a>R 教程

除非另行说明，否则教程适用于 SQL Server 2016 R Services，开发和应适用于 SQL Server 自 2017 年 1 机器学习服务无需重大更改。

所有教程都请广泛使用 RevoScaleR 包中的功能的 SQL Server 计算上下文。

+ [数据科学深入了解 R 和 SQL Server](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)

  了解如何使用 RevoScaleR 包中的函数。 R 和 SQL Server 和交换机之间移动数据计算上下文，以满足特定的任务。 创建模型和绘图，和你的开发环境与数据库服务器之间移动它们。

  **受众：** 为数据科研人员或开发人员已熟悉 R 语言中，并想要了解有关增强的 R 包和 Microsoft R 由 Revolution Analytics 中的函数。

  **要求：** R 了解一些基本知识。 对 SQL Server R Services 或与。 机器学习服务的服务器的访问安装程序帮助，请参阅[先决条件](#bkmk_Prerequisites)。

+ [针对 SQL 开发人员的数据库中 R 分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

  生成和部署一个完整的 R 解决方案，仅使用[!INCLUDE[tsql](../../includes/tsql-md.md)]工具。

  重点将解决方案移到生产环境。 学习如何将 R 代码包含在存储过程中，将 R 模型保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中，以及参数化调用 R 模型用于预测。

  **受众：** SQL 开发人员、 应用程序开发人员或 SQL 专业人员支持 R 解决方案并且想要了解如何将 R 模型部署到 SQL Server。

  **要求：** 不需要任何 R 环境。 提供所有 R 代码，你可以构建完整解决方案仅使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]和大家熟悉的商业智能和 SQL 开发工具。 但是，R 一些基本知识将会很有帮助。

  使用 R 语言安装并启用必须访问 SQL Server。 安装程序帮助，请参阅[先决条件](#bkmk_Prerequisites)。

+ [快速入门： 在 T-SQL 中使用 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)

  本快速入门教程介绍如何使用 R 中的基本语法[!INCLUDE[tsql](../../includes/tsql-md.md)]。

  了解如何从 T-SQL 调用 R 运行时，将 R 函数包装在 SQL 代码，并运行将 R 输出和 R 模型保存到 SQL 表的存储的过程。

  **受众：** 的熟悉功能，并且想要了解从存储过程调用 R 的基础知识的人员。

  **要求：** R 或所需的 SQL 不知道。 但是，你需要 SQL Server Management Studio 或另一个客户端，可以连接到数据库并运行 T-SQL。 我们建议免费[MSSQL 扩展 Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)如果你不熟悉 T-SQL 查询。

  你还必须具有 SQL Server R Services 或使用已启用的 R 的机器学习服务的服务器的访问。 安装程序帮助，请参阅[先决条件](#bkmk_Prerequisites)。

+ [数据科学端到端演练](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

  从开头到末尾，获取数据并将其保存到 SQL Server、 分析使用 R 数据和生成关系图演示数据科学过程。

  你将了解如何将图形之间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 R，以及在 T-SQL 中的使用 R 函数比较特征工程。 最后，您将学习如何使用中的预测模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]批量计分和单行评分。

  **受众：** 的熟悉使用 R 和 SQL Server Management Studio 等开发人员工具的用户。

  **要求：** 应该有权访问的 R 开发环境，并且知道如何运行 R 命令。 使用 PowerShell 需要下载纽约市 taxi 数据集。 你必须有权使用 SQL Server R Services 或使用已启用的 R 的机器学习服务的服务器。 安装程序帮助，请参阅[先决条件](#bkmk_Prerequisites)。

## <a name ="bkmk_samples"></a>产品示例

由 SQL Server 开发团队，以突出显示你可以在实际应用程序中使用嵌入的分析的各种方法提供了这些示例和演示。

+ [生成使用 R 和 SQL Server 的预测模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction)

  了解如何 ski 租赁业务可能使用机器学习来预测将来出租，它可帮助企业版计划和员工，以满足将来需求。

+ [执行客户群集使用 R 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/)

  使用无人监督的学习到段客户基于销售数据。

## <a name="bkmk_Prerequisites"></a>先决条件

若要使用这些教程和示例，你必须安装以下服务器产品之一：

+ SQL Server 2016 R Services （数据库）
  
  支持。 请确保安装机器学习功能，然后再启用外部脚本。

+ SQL Server 自 2017 年 1 机器学习服务 （数据库）
  
  支持 R 或 Python。 你必须选择机器学习功能和语言后，若要安装，然后启用外部脚本。

运行 SQL Server 安装程序之后, 不要忘记以下重要步骤：

+ 通过运行启用外部脚本执行功能 `sp_configure 'external scripts enabled', 1`
+ 重新启动服务器
+ 请确保调用外部运行时服务的必需的权限
+ 确保你的 SQL 登录名或 Windows 用户帐户具有所必需的权限连接到服务器，以读取数据，并创建此示例要求任何数据库对象

如果你遇到问题，请参阅此文章了解遇到的一些常见问题：[疑难解答机器学习服务](../machine-learning-troubleshooting-faq.md)
