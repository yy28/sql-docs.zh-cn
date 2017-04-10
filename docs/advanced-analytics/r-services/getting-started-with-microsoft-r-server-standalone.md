---
title: "Microsoft R Server（独立版）入门 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "r-server"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 52347d0d-ce60-4bb8-98d2-6163e87716b0
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 16
---
# Microsoft R Server（独立版）入门
  Microsoft R Server（独立版）可帮助将流行的开源 R 语言引入企业，以实现高性能分析解决方案以及与其他业务应用程序的集成。  
  
## Microsoft R Server 是什么？  
 Microsoft R Server（独立版）包括由 Revolution Analytics 开发的增强型 R 包，并支持与多种不同数据源的连接，例如 Hadoop、Teradata 等。 通过安装此独立服务器，你可以创建用于运行复杂、可扩展 R 作业的服务器环境。  
  
## 使用 Microsoft R 服务器 （独立） 的好处  
 R 是世界上最强大的用于统计计算、机器学习和图形的编程语言，而且受到蓬勃发展的全球社区的用户、开发人员和参与者的支持。 从以往来看，在企业设置中使用 R 具有一定的挑战，尤其当数据量越来越大或在你需要将解决方案部署到产品环境中时。 Microsoft R Server 解决了 R 代码的部署和操作化的问题。  
  
 Microsoft R Server 可以安装在任何 Windows 计算机上，并包含所有的多个 R 包和连接工具来启用远程计算上下文并支持可扩展、 可并行化解决方案。  
  
 Microsoft R 服务器 （独立） 支持这些方案︰  
  
-   **使用中心服务器实施 R 解决方案**  
  
     此独立服务器可为你提供改进的 R 性能，而无需依靠 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 可以在服务器上的便携式计算机或开发计算机上可能会受到限制的资源而被执行复杂或占用大量资源的计算。  
  
     您还可以集中在一起的作业，例如，如果需要针对在生产中，预测模型评分或使用 R 服务器作为 R 的单一联系点绘制，并且在报告中使用的预测。 
     
     我们还建议您安装 R 服务器 （独立） SQL Server 计算机上如果需要频繁地运行 SQL Server 的上下文之外的 R。
  
-   **启用功能更加强大的数据浏览和预测建模**  
  
     数据科学家可以使用任何客户端工作站和任何 R 开发工具来生成 R 解决方案。 如果解决方案使用 RevoScaleR 包 API，那么可以在服务器上执行计算，通常该服务器具有更大的处理能力和内存。 因此你的解决方案可以处理更大的数据集并利用多线程、多核和多进程计算。  
  
## 如何获取它？  
 有关安装说明，请参阅 [Create a Standalone R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md)。 可以使用安装的所有组件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序。  
  
## 安装其他 R 工具  
 如果没有一个首选的 R 的开发环境，有很多选项。 有关详细信息，请参阅 [安装或配置 R 工具](../../advanced-analytics/r-services/setup-or-configure-r-tools.md)。 
 
 用于连接到 Microsoft R Server 或 SQL Server R Services 从数据科学工作站，我们建议免费 [Microsoft R Client](http://aka.ms/rclient/download) （下载）。  
  
## Microsoft R 服务器 （独立） 上运行 R 脚本  
 您设置的服务器组件并安装您最喜欢的 R IDE 后，可以开始开发您的解决方案使用 RevoScaleR 包。 通过这些 API 将 R 命令发送到远程服务器执行。  
  
-   [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started)︰ 通过探索此集合提供高性能的可分发分析函数并缩放到 R 解决方案来开始。 包括可并行化版本的许多最受欢迎的 R 建模包，如 k 平均值聚类分析、 决策树和决策林和数据操作的工具。 您可以使用 HPC 来构建您自己的并行算法。  
    
-   [DeployR](https://msdn.microsoft.com/microsoft-r/deployr-about)︰ 此可选框架提供了对 R 编程人员使用 Java、 JavaScript 或.Net 将集成的第三方包的输出的 R 分析工具。  

您可以使用各种格式，包括 SAS、 SPS、 Hadoop 和文本的文件中的数据。 可以分析数据中的位置，或有效地将数据移到本地 R 开发环境使用.xdf 文件格式。  
  
若要开始使用 R 服务器，请参阅 MSDN Library 中的本指南︰ [R Server-入门](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started)  
  
 有关如何使用 ScaleR 包的信息，请参阅 [25 函数中的 R 教程](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started#an-r-tutorial-in-25-functions-or-so)  
  
## 另请参阅  
 [SQL Server R Services 入门](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  