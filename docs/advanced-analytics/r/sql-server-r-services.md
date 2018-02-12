---
title: "SQL Server 机器学习服务 |Microsoft 文档"
ms.date: 12/04/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Active
ms.openlocfilehash: 37362b8a3f6d8b41fe6b52f8445b9ba08ca54aa3
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2018
---
# <a name="sql-server-machine-learning-services"></a>SQL Server 机器学习服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 自 2017 年 1 机器学习服务 (以前 SQL Server 2016 R Services) 提供一个平台，用于开发和部署发掘新见解的智能应用程序。 由于与集成机器学习[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，你可以使数据接近的分析，并消除成本和与数据移动相关的安全风险。
  
+ 在 SQL Server 2016 中，可以轻松地开发和部署基于流行的 R 语言的数据科学解决方案。 

    功能包括[Microsoft R](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)库，为你的 R 解决方案和中的最先进的算法提供新的可伸缩性和性能[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)。
+ 在 SQL Server 自 2017 年，可以使用 R 和 Python 开发并实施数据科学解决方案。 

    [Revoscalepy](../python/what-is-revoscalepy.md) Python 库提供远程计算上下文和可伸缩性 RevoScaleR 媲美。

SQL Server 支持通过一组全面的工具和技术的机器学习工作负载改进的性能、 安全性和可管理性。 你可以部署 R 或 Python 使用方便的解决方案，熟悉 SQL 方法和工具。 只需使用[!INCLUDE[tsql](../../includes/tsql-md.md)]从生产应用程序，可以生成模型或检索视觉对象调用 R 或 Python 运行时。 如果你具有已定型模型，你可以通过使用仅 T-SQL，从该生成预测[本机评分](../sql-native-scoring.md)。

## <a name="machine-learning-in-sql-server-2017"></a>SQL Server 自 2017 年中的机器学习

+ 安装**机器学习服务 （数据库）**期间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装程序以在启用安全 R 或 Python 脚本执行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]计算机。
  
    选择此功能，则在数据库引擎来支持以 R 或 Python 编写的代码的执行中安装扩展。 创建新的服务， [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]，若要管理的外部运行时之间的通信和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。
  
+ 安装**Microsoft 机器学习 Server （独立）**如果你不需要作为计算上下文中使用 SQL Server 的单独计算机上。 机器学习服务器包括相同的机器学习组件，以及执行可伸缩的分布式机学习作业作为 web 服务的能力。
  
+ 安装[Microsoft R 客户端](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)开发可部署到 SQL Server 或在 Windows、 Linux 或 Hadoop 的机器学习服务器的解决方案的远程计算机上。

## <a name="machine-learning-in-sql-server-2016"></a>SQL Server 2016 中的机器学习

+ 安装**R Services （数据库）**在 SQL Server 2016 上启用安全 R 脚本执行的安装过程[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]计算机。
  
    当你选择了此功能时，可以具有运行 R 脚本使用 SQL Server 作为计算上下文，或在存储过程中运行 R 脚本的能力。
  
+ 安装**Microsoft R Server （独立）**从 SQL Server 2016 安装程序，可用于开发或部署 R 解决方案的单独计算机上安装的 R 组件。

## <a name="how-to-get-started"></a>如何开始

SQL Server 安装程序提供两个选项：

+ 与 SQL Server 集成的数据库中分析功能，是的安装或
+ 安装支持的 SQL Server 实例情况下的大规模机器学习的独立版本的机器学习服务器 （或 Microsoft R Server）。

如果你需要在其中运行 R 代码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，通过使用存储的过程或通过使用 SQL Server 实例作为计算上下文，你必须安装[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中所述[安装指南](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)。 此选项提供最大数据安全和与 SQL Server 工具的集成。

Microsoft 机器学习 Server （独立） 是为使用而设计的一个单独选项[Microsoft R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)和[相关 Python 库](../python/what-is-revoscalepy.md)未运行 SQL Server 的 Windows 计算机上。 此选项需要 SQL server 企业版许可证。
    
我们建议你在便携式计算机或用于开发，其他远程计算机上安装机器学习 Server （独立），并使用该计算机创建和测试可以轻松地部署到的实例的机器学习解决方案[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，它是运行机器学习服务\(数据库中\)或其他支持的计算上下文。
  
你还可以使用**mrsdeploy**随机器学习服务器来发布和分发 R 和 Python 作业作为 web 服务一起安装的包。

## <a name="additional-resources"></a>其他资源

+ [SQL Server 计算机学习 Services 入门](../../advanced-analytics/r/getting-started-with-sql-server-r-services.md)
 
    描述 R 与 SQL Server 使用的常见的方案

+ [设置 SQL Server 计算机学习 Services 或 R 服务数据库中](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

    SQL Server 安装的一部分安装 R 和关联的数据库组件
  
+ [SQL Server 和 R 教程](../../advanced-analytics/tutorials/sql-server-r-tutorials.md)

    了解如何在 R 代码中创建 SQL Server 数据源，以及如何使用远程计算上下文。 面向 SQL 开发人员的其他教程演示如何在 SQL Server 中定型和部署 R 模型。
