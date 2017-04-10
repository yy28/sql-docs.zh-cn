---
title: "SQL Server R Services 教程 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 5ccc75f6-6703-47d9-b879-9a740569b45e
caps.latest.revision: 31
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 27
---
# SQL Server R Services 教程
使用这些教程来了解 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 和其支持的数据科学方案，包括：

+ 在 R 中开发模型并将其部署到 SQL Server
+ 通过将由数据科学家开发的 R 解决方案部署到服务器或其他生产环境来实现 R 代码。
+ 在 R 和 SQL Server 之间移动数据
+ 远程和本地计算上下文的使用方法
  

## <a name="a-namebkmkend-to-endadeveloping-an-end-to-end-advanced-analytics-solution"></a><a name="bkmk_end-to-end"></a>开发端到端高级分析解决方案  

[数据科学端到端演练](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md) 

体验数据科学端到端过程，从数据采集和分析到评分。 学习如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的数据，以及如何通过将模型保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对其进行实现。  
使用 PowerShell 将纽约市出租车数据集导入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，并使用 R 浏览数据。 

然后构建预测模型并将 R 模型部署到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，以便以批量或单预测模式进行计分。 

  
本教程适用于对 R 以及 PowerShell 和 SQL Server Management Studio 等开发人员工具具有一定熟悉程度的人员。 用户应有权访问 R 开发环境并熟悉 R 命令。 
  
## <a name="a-namebkmkdatascienceadata-science-deep-dive"></a><a name="bkmk_dataScience"></a>对数据科学的深入探讨  

[RevoScaleR 和 SQL Server 入门](http://go.microsoft.com/fwlink/?LinkID=691640&clcid=0x809)  

本演练适用于已熟悉 R 语言且想要了解 Revolution Analytics 提供的 Microsoft R 中的增强型 R 包和函数的数据科学家或开发人员。 

你将学习如何使用 ScaleR 包中的函数在 R 和 SQL 之间移动数据，以及切换计算上下文来适应特定的任务。 创建一些模型和图形，并将其在开发环境和 SQL Server 之间进行移动。  
  
本教程适用于使用 R，并且想要了解有关 RevoScaleR 和 SQL Server 可以如何改进 R 体验的详细信息的人员。

## <a name="in-database-advanced-analytics-for-the-sql-developer"></a>适用于 SQL 开发人员的数据库内高级分析  
  
[适用于 SQL 开发人员的数据库内高级分析（教程）](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)

使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 生成并部署一个完整的高级分析解决方案。 此示例重点介绍如何将开放源代码 R 语言与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库引擎集成。 学习如何将 R 代码包含在存储过程中，将 R 模型保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中，以及参数化调用 R 模型用于预测。 
  
本教程适用于支持 R 解决方案并且想要了解如何将 R 模型部署到 SQL Server 的 SQL 开发人员、应用程序开发人员或 SQL DBA。  不需要任何 R 环境；提供了所有的 R 代码，并且可以仅使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、熟悉的商业智能和 SQL 开发工具来生成完整的解决方案。   

## <a name="use-r-services-in-an-application"></a>在应用程序中使用 R Services

[Build an intelligent app with SQL Server and R](https://www.microsoft.com/sql-server/developer-get-started/r)（使用 SQL Server 和 R 生成智能应用）

在本教程中，将介绍雪橇租赁公司可如何使用机器学习来预测未来的租赁情况，这有助于合理制定业务和人员计划以满足未来的需求。


## <a name="using-r-code-in-t-sql"></a>在 T-SQL 中使用 R 代码  

[在 Transact-SQL 中使用 R 代码 (SQL Server R Services)](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)  

本系列简短的独立示例演示了在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中使用 R 的基本语法。 

你将学习如何从 SQL 调用 R 运行时，了解数据类型在 R 和 SQL 之间的主要差异，打包 SQL 代码中的 R 函数和运行将 R 输出保存到 SQL 表的存储过程。
  
本教程适用于刚使用 R 服务并且想要了解如何使用 T-SQL 调用 R 的基础知识的人员。 无需 R 体验；但用户应了解如何使用 SQL Server Management Studio，或了解任何其他可连接到数据库和运行简单 T-SQL 查询的工具。

  
## <a name="a-namebkmkprerequisitesaprerequisites"></a><a name="bkmk_Prerequisites"></a>先决条件
  
若要运行这些教程，则必须下载并安装“R Services (数据库中)”，如[设置 SQL Server R 服务](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)所述

运行 SQL Server 安装程序之后，请不要忘记以下附加步骤：
+ 通过运行 sp_configure 启用 R 服务
+ 重新启动服务器
+ 确保调用 R 运行时的服务具有必要的权限
+ 确保将用于 R 代码的 SQL 登录名或 Windows 用户帐户具有连接到服务器及其数据库所必需的权限

如果遇到问题，请参阅文章[升级和安装 SQL Server R 服务](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)以解决一些常见问题

如果尚未有一个首选的 R 开发环境，则可以从安装以下其中一种工具开始：

+ [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-get-started)
+ [用于 Visual Studio 的 R 工具](https://www.visualstudio.com/vs/rtvs/)

请注意，标准 R 库不足以使用这些教程；R 开发环境和运行 R 的 SQL Server 计算机必须具有来自 Microsoft 的 ScaleR 包。 有关 Microsoft R 中的内容的详细信息，请参阅文章：[Microsoft R 产品](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started#compare-prods)。

## <a name="additional-resources"></a>其他资源

学完这些教程时，使用以下链接可查看更高级的方案和示例。
  
### <a name="end-to-end-solution-templates-for-key-machine-learning-tasks"></a>用于关键机器学习任务的端到端解决方案模板  

[Machine Learning Templates with SQL Server 2016 R Services](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/)（具有 SQL Server 2016 R Services 的机器学习模板）。  

Microsoft 机器学习团队已提供了一组可自定义模板，有助于快速开始针对这些主要机器学习任务的机器学习解决方案：  
* 欺诈检测  
* 自定义改动预测  
* 预测维护  
  
提供了所有的 T-SQL 和 R 代码，以及如何使用 SQL Server 存储过程定型和部署模型用于评分的说明。 

### <a name="sample-data-and-sample-scripts"></a>示例数据和示例脚本  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的产品示例可以从 Microsoft 下载中心获得。 若要仅获取 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 示例，请选择该 zip 文件，并打开“高级分析”文件夹。  部分说明适用于早期版本，但其中还演示了根据本福特定律检测保险欺诈，并简单演练了针对非常小的数据集（Iris 数据集）的预测模型以辅助演示。
  
[SQL Server 2016 产品示例](https://www.microsoft.com/en-us/download/details.aspx?id=49502)  
### <a name="learn-more-about-r"></a>了解有关 R 的详细信息  
要大致了解有关 R 的更多信息，请参阅此处列出的许多优质资源之一： [R Language Resources](http://revolutionanalytics.com/r-language-resources)（R 语言资源）。  
  
有关 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]提供的 R 包的其他信息，请参阅  [Revolution Analytics site](http://go.microsoft.com/fwlink/?LinkId=691541)（Revolution Analytics 站点）。  
  
这篇博客文章概括了使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 提供的 R 包和函数连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的过程，并包含了示例代码： [Using R inside SQL Server](http://blog.revolutionanalytics.com/2015/10/previewing-using-revolution-r-enterprise-inside-sql-server.html)（在 SQL Server 内使用 R）。  
  
## <a name="see-also"></a>另请参阅  
[SQL Server R 服务入门](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
[SQL Server R 服务功能和任务](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)  
  
