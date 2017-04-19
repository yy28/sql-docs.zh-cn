---
title: "不同 SQL Server 版本中 R 功能的差异 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8b33a3e2-04d3-4bad-9335-9568ae09db0b
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bf58c40359c717f7195570699e2d94435c8a0855
ms.lasthandoff: 04/11/2017

---
# <a name="differences-in-r-features-between-editions-of-sql-server"></a>不同 SQL Server 版本中 R 功能的差异
  以下版本的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中和 SQL Server vNext 中提供了 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]：  
  
-   **Enterprise Edition**  
    
     包括两个 R Services（SQL Server 中的数据库内分析，以 Windows 上的 R Server（独立版）），可用于连接到各种数据库以及大规模提取分析数据，但无法在数据库内运行。  

     无限制。 通过并行化和流式处理优化性能与可伸缩性。 支持使用 **ScaleR** 函数分析无法装入可用内存的大型数据集。  
     
     更新版本的 Microsoft R Server 包括操作化引擎 （以前称为 DeployR）的改进版本，该引擎支持快速安全的部署和 R 解决方案共享。 有关详细信息，请参阅 [Operationalize](https://msdn.microsoft.com/microsoft-r/operationalize/about)（操作化）。
  
     SQL Server 中的数据库内分析支持使用外部脚本的资源调控来自定义服务器资源用量。  
  
-   **Developer Edition**  

    功能与 Enterprise Edition 相同；但是，无法在生产环境中使用 Developer Edition。  

  
  
-   **Standard Edition**  
  
     包括 Enterprise Edition 随附的所有数据库内分析功能，但灵活的资源调控功能除外。 性能和规模也受到限制：可处理的数据必须能够装入服务器内存，并且处理仅限于单个计算线程，即使使用 **ScaleR** 函数，也是如此。
  
-   **Express Editions**  
  
     只有包含高级服务的 Express Edition 才提供 R Services。 性能限制与 Standard Edition 类似。  
  
 有关其他产品功能的详细信息，请参阅 [SQL Server 2016 的版本和支持的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。 
> [!NOTE]
>
> + 所有版本都随附 Microsoft R Open。
> + Microsoft R Client 适用于所有版本。
  
## <a name="enterprise-edition"></a>Enterprise Edition  
 在硬件相同的前提下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中 R 解决方案的性能预期优于任何传统 R 实现，因为 R 可以使用服务器资源运行，有时可以 **ScaleR** 函数分配到多个进程。  
  
 如果分别在 Enterprise Edition 与 Standard Edition 中运行相同的 R 函数，用户预期也会感受到性能和可伸缩性具有很大的差异。 原因包括支持并行处理、流式处理，以及增加了可用于处理 R 工作进程的线程数。  
  
 但是，即使是在相同的硬件上，性能也可能会受到 R 代码外部的许多因素影响，包括服务器资源争用需求、创建的查询计划类型、架构更改、更新统计信息或创建新查询计划的需要、碎片，等等。 有可能某个包含 R 代码的存储过程在一种工作负荷几秒钟即可完成运行，但运行其他服务时却要花费几分钟才能完成运行。  因此，我们建议在量化 R 的作业性能时，监视服务器性能的多个方面，包括远程计算上下文的网络。  

此外，我们建议配置[资源调控器](../../relational-databases/resource-governor/resource-governor.md)（Enterprise Edition 中已提供），来自定义在重度服务器工作负荷下排定 R 作业优先级或或处理 R 作业的方式。 可以定义分类器函数来指定 R 作业的源并排定某些工作负荷的优先级、限制 SQL 查询使用的内存量，以及根据工作负荷控制使用的并行进程数。  
  
## <a name="developer-edition"></a>Developer Edition  
 Developer Edition 提供的性能与 Enterprise Edition 相当；但是，不支持在生产环境中使用 Developer Edition。  
  
  
## <a name="standard-edition"></a>Standard Edition  
 在硬件配置相同的前提下，与标准 R 包相比，即使是 Standard Edition 也能提供一定的性能优势。  
  
 但是，Standard Edition 不支持资源调控器。 使用资源调控是自定义服务器资源，使其支持各种 R 工作负荷（例如模型训练和评分）的最佳方式。  
  
 此外，与 Enterprise Edition 和 Developer Edition 相比，Standard Edition 提供的性能和可伸缩性有限。 具体而言，Standard Edition 包含所有 **ScaleR** 函数和包，但启动和管理 R 脚本的服务在可用的进程数方面受到限制。 此外，脚本处理的数据必须能够装入内存。  
  
  
## <a name="express-edition-with-advanced-services"></a>包含高级服务的 Express Edition  
 Express Edition 的限制与 Standard Edition 相同。  
  
## <a name="see-also"></a>另请参阅  
[SQL Server 2016 的各版本和支持的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md) 

  

