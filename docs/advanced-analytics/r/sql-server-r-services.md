---
title: "SQL Server 机器学习服务 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: 38
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e8c384b7fba553175767aaf7c439207771b31e6b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="sql-server-machine-learning-services"></a>SQL Server 机器学习服务

  SQL Server 自 2017 年 1 机器学习服务 (以前 SQL Server 2016 R Services) 提供一个平台，用于开发和部署发掘新见解的智能应用程序。 可以使用丰富且功能强大的 R 语言以及许多来自社区的包来创建模型，并使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据生成预测。
  
  由于与集成机器学习[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，你可以使数据接近的分析，并消除成本和与数据移动相关的安全风险。
  
SQL Server 支持的开放源代码 R 语言与一组全面的工具和技术的提供优异的性能、 安全性、 可靠性和可管理性。 你可以部署 R 解决方案使用便利、 熟悉 SQL 工具和生产应用程序可以调用 R 运行时和检索预测和视觉对象使用[!INCLUDE[tsql](../../includes/tsql-md.md)]。 你还可以获取[Microsoft R](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)库以改进的缩放和 R 解决方案，包括 RevoScaleR、 revoscalepy 和 MicrososftML 的性能。
  
可通过 SQL Server 安装程序安装服务器和客户端组件。
  
## <a name="machine-learning-in-sql-server-2017"></a>SQL Server 自 2017 年中的机器学习

+ 安装**机器学习服务 （数据库）**期间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装程序以在启用安全 R 或 Python 脚本执行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]计算机。
  
    选择此功能，则在数据库引擎来支持以 R 或 Python 编写的代码的执行中安装扩展。 创建新的服务， [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]，若要管理的外部运行时之间的通信和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。
  
+ 安装**Microsoft 机器学习 Server （独立）**如果你不需要作为计算上下文中使用 SQL Server 的单独计算机上。 机器学习服务器包括相同的机器学习组件，以及可缩放的分布式执行的机器学习作业作为 web 服务的 mrsdeploy 包。
  
+    安装[Microsoft R 客户端](https://docs.microsoft.com/r-server/r-client/what-is-microsoft-r-client)开发可部署到 SQL Server 或在 Windows、 Linux 或 Hadoop 的机器学习服务器的解决方案的远程计算机上。

## <a name="machine-learning-in-sql-server-2016"></a>SQL Server 2016 中的机器学习

+ 安装**R Services （数据库）**在 SQL Server 2016 上启用安全 R 脚本执行的安装过程[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]计算机。
  
    当你选择了此功能时，可以具有运行 R 脚本使用 SQL Server 作为计算上下文，或在存储过程中运行 R 脚本的能力。
  
+   安装**Microsoft R Server （独立）**从 SQL Server 2016 安装程序以设置用于 developin R 解决方案的单独计算机上的 R 组件。


## <a name="which-type-of-machine-learning-service-do-i-need"></a>是否需要哪种类型的机器学习服务？

+ 如果你需要在其中运行 R 代码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，通过使用存储的过程或通过使用 SQL Server 实例作为计算上下文，你必须安装[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]所述[此处](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。

+ Microsoft 机器学习 Server （独立） 是为使用而设计的一个单独选项[Microsoft R](https://docs.microsoft.com/r-server/r-reference/introducing-r-server-r-package-reference)和[相关 Python 库](../python/what-is-revoscalepy.md)未运行 SQL Server 的 Windows 计算机上。 它，但是，需要企业版许可证的 SQL Server。
    
    我们建议你在便携式计算机或用于开发，其他远程计算机上安装 Microsoft 机器学习 Server （独立版），并使用该计算机创建和测试可以轻松地部署到的实例的计算机学习解决方案[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]运行机器学习服务\(数据库中\)或其他支持的计算上下文。
  
    你还可以使用**mrsdeploy**随机器学习服务器来发布和分发 R 和 Python 作业作为 web 服务一起安装的包。

## <a name="additional-resources"></a>其他资源

+ [SQL Server R 服务入门](../../advanced-analytics/r/getting-started-with-sql-server-r-services.md)
 
    描述 R 与 SQL Server 使用的常见的方案

+ [设置 SQL Server R Services（数据库内）](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

    SQL Server 安装的一部分安装 R 和关联的数据库组件
  
+ [SQL Server R 教程](../../advanced-analytics/tutorials/sql-server-r-tutorials.md)

    了解如何在 R 代码中创建 SQL Server 数据源，以及如何使用远程计算上下文。 面向 SQL 开发人员的其他教程演示如何在 SQL Server 中定型和部署 R 模型。

