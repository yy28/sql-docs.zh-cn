---
title: "SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: 38
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 36
---
# SQL Server R Services
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 提供了一个平台，用于开发和部署可发掘新见解的智能应用程序。 可以使用丰富且功能强大的 R 语言以及许多来自社区的包来创建模型，并使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据生成预测。 因为 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 已将 R 语言与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]集成，你可以保持与数据接近的分析结果，同时清除与数据移动相关的成本和安全风险。  
  
 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 支持具有一套综合性 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具的开放源 R 语言，还支持可提供优异性能、安全性、可靠性和易管理性的技术。 你可以使用便利、熟悉的工具部署 R 解决方案，生产应用程序可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]调用 R 运行时和检索预测与可视化对象。 还可获取 [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) 库，改进 R 解决方案的规模和性能。  
  
可通过 SQL Server 安装程序安装服务器和客户端组件。  
  
+   **R Services (In-Database)：** 在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的过程中安装此功能可在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机上启用安全的 R 脚本执行。  
  
     如果选择了此功能，将在数据库引擎中安装扩展来支持 R 脚本执行，并创建一个新服务 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]，用于管理 R 运行时与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例之间的通信。  
  
+   **Microsoft R Server（独立）：**开放源 R 的分发，它结合了支持并行处理的专有包和其他性能改。 R Services（数据库内）和 Microsoft R Server（独立）包括基础 R 运行时和包，以及用于增强连接性和性能的 **ScaleR** 库。 
  
+    [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/index#mrc) 可作为一种独立的免费安装程序。  可使用 Microsoft R Client 开发解决方案，可将此类解决方案部署到在 SQL Server 上运行的 R Services，或部署到在 Windows、Teradata 或 Hadoop 上运行的 Microsoft R Server。 
     

  > [!NOTE] 如果需要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中运行 R 代码，请确保按[此处](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)的说明安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。
  >  
  > Microsoft R Server \(独立\) 是一个独立选项，专为使用不运行 SQL Server 的 Windows 计算机上的 ScaleR 库而设计。 
>   
>  但是，如果有企业版，建议在用于 R 开发的笔记本电脑或其他计算机上安装 Microsoft R Server \(独立\)，创建可轻松部署到运行 R Services \(数据库内\)的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的 R 解决方案。
  
## <a name="additional-resources"></a>其他资源  
  
 [SQL Server R Services 入门](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)   
 介绍配合使用 R 和 SQL Server 的常见方案。  
  
[设置 SQL Server R Services（数据库内）](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
在 SQL Server 安装过程中安装 R 及关联的数据库组件。  
  
[SQL Server R Services 教程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
了解如何在 R 代码中创建 SQL Server 数据源，以及如何使用远程计算上下文。 面向 SQL 开发人员的其他教程演示如何在 SQL Server 中定型和部署 R 模型。  
  
## <a name="see-also"></a>另请参阅  
  
 [Microsoft R Server（独立版）入门](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
 
 [设置独立 R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md) 
  