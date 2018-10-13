---
title: SQL Server Python 教程 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 541675c22ddbe347f67119d8cba82f75955382e6
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2018
ms.locfileid: "48877981"
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

## <a name="bkmk_Prerequisites"></a>先决条件

若要使用这些教程，必须具有 SQL Server 2017 中，并且你必须显式安装，然后启用该功能，机器学习服务 （数据库内）。 

SQL Server 2017 支持 R 和 Python 语言，但既不是安装或默认情况下启用。 运行 Python 需要启用可扩展性框架，并为要安装的语言选择 Python。 

### <a name="post-installation-configuration-tips"></a>安装后配置提示

在运行 SQL Server 安装程序之后, 您可能需要执行一些附加步骤以确保 Python 和 SQL Server 进行通信：

+ 通过运行启用外部脚本执行功能`sp_configure 'external scripts enabled', 1`。
+ 重新启动服务器。 
+ 打开**Services**面板来检查是否已启动快速启动板。 
+ 请确保调用外部运行时的服务具有必要的权限。 有关详细信息，请参阅[启用隐式身份验证](../security/add-sqlrusergroup-to-database.md)。
+ 对于 SQL Server，打开防火墙上的端口并启用所需的网络协议。
+ 请确保你的 SQL 登录名或 Windows 用户帐户具有必需的权限连接到服务器，以读取数据，并创建此示例要求任何数据库对象。

请参阅本文有关的一些常见问题：[故障排除的机器学习服务](../machine-learning-troubleshooting-faq.md)

### <a name="resource-management"></a>资源管理

可以在同一台计算机上安装 R 和 Python，但同时运行可能需要大量资源。 如果出现"内存不足"错误，或运行机器学习作业是主体服务器的用途，可以减少分配给数据库引擎的内存量。 有关详细信息，请参阅[管理和监视 SQL Server 中的 Python](../python/managing-and-monitoring-python-solutions.md)。

## <a name="see-also"></a>请参阅

[SQL Server 的 R 教程](sql-server-r-tutorials.md)
