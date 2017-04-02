---
title: "在 R 功能的 SQL Server 各版本之间的差异 | Microsoft Docs"
ms.custom: ""
ms.date: "01/19/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8b33a3e2-04d3-4bad-9335-9568ae09db0b
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# 在 R 功能的 SQL Server 各版本之间的差异
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可用于以下版本的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
-   **Enterprise Edition**  
    
     包括两个 R 服务，用于在 SQL Server 2016，以及在 Windows 上，这可以用于连接到各种数据库和请求数据以进行分析在规模较大，但它不会运行数据库中的 R 服务器 （独立） 中的数据库中分析。 此外包括 **DeployR**, ，它可以用于将 R 脚本和模型部署为 Web 服务。  

     无限制。 优化的性能和可扩展性通过并行化和流式处理。 通过使用不适合在可用内存的大型数据集的 Suopprts 分析 **ScaleR** 函数。  
  
     在 SQL Server 中的数据库中分析支持资源调控的外部脚本以自定义服务器资源使用情况。  
  
-   **开发人员版**  

    Enterprise Edition 与相同的功能但是，不能在生产环境中使用开发人员版。  

  
  
-   **Standard Edition**  
  
     已在数据库中分析的所有功能，都附带 Enterprise Edition 除外灵活的资源调控。 性能和可扩展性也得到限制︰ 可处理的数据具有服务器内存中容纳不下，即使在使用时，处理仅局限于单个计算线程 **ScaleR** 函数。
  
-   **速成版**  
  
     只有 Express Edition with Advanced Services 提供 R 服务。 性能限制是类似于标准版。  
  
 有关其他产品功能的详细信息，请参阅 [支持的 SQL Server 2016 版本功能](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  

> [!NOTE]
>
> + Microsoft R Open 将包含在所有版本。
> + Microsoft R 客户端可以使用所有版本。
  
## Enterprise Edition  
 R 中的解决方案的性能 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 预期为通常比任何常规的 R 实现，因为可以使用服务器资源运行 R 指定相同的硬件，有时分发到多个进程使用更好 **ScaleR** 函数。  
  
 用户还可能会看到性能和可伸缩性，如果在 Enterprise Edition vs 中运行相同的 R 函数很大的差异。Standard Edition。 原因包括支持并行处理、 流式处理，以及增加可用于处理的 R 工作线程的线程。  
  
 但是，即使在相同的硬件上性能可能受到许多因素包括服务器上的资源相互竞争的要求、 创建的查询计划的类型、 架构已更改，在 R 代码的外部需要更新统计信息或创建新的查询计划、 碎片，等等。 可能的存储的过程包含 R 代码可能会以秒为单位在一个工作负荷下运行，但采取分钟时正在运行的其他服务。  因此，我们建议您监视服务器性能，包括网络连接的远程计算上下文，当量化 R 的作业性能的多个方面。  

我们还建议您配置 [资源调控器](../../relational-databases/resource-governor/resource-governor.md) （适用于企业版） 以自定义 R 作业中设置优先级或处理大量的服务器工作负荷下的方式。 你可以定义分类器函数来指定 R 作业的源并按优先级排列某些工作负荷、 限制由 SQL 查询使用的内存量和控制使用基于工作负荷的并行流程的数量。  
  
## 开发人员版  
 Developer 版提供了等效的 Enterprise Edition 的性能但是，对于生产环境不支持使用开发人员版。  
  
  
## Standard Edition  
 甚至标准版应提供某些性能优势，与标准的 R 包，提供相同的硬件配置相比。  
  
 但是，标准版不支持资源调控器。 使用资源调控是自定义服务器的资源来支持各种的 R 工作负荷，如模型定型集和评分的最佳方法。  
  
 标准版还提供了有限的性能和可伸缩性相比 Enterprise edition 和 Developer Edition。 具体而言，所有 **ScaleR** 函数和包包括标准版中，但它可以使用的进程数有限制的服务的启动和管理 R 脚本。 此外，该脚本所处理的数据必须能够容纳在内存中。  
  
  
## Express Edition with Advanced Services  
 Express Edition 是为标准版相同的限制。  
  
## 另请参阅  
 [SQL Server 2016 各个版本支持的功能](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
  
  