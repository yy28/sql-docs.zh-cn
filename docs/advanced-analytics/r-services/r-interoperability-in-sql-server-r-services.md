---
title: "SQL Server R 服务中的 R 互操作性 | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0506b950-34b3-4f11-8e2f-d067a58015bd
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# SQL Server R 服务中的 R 互操作性

本主题重点介绍运行中的 R 的机制 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], ，并介绍 Microsoft R 和开放源代码 R.之间的差异有关其他组件的信息，请参阅 [SQL Server 中的新组件](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)。

### 开放源代码 R 的组件

[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 包括基本多个 R 包和工具的完整分发。 有关什么是附带的基本分布的详细信息，请参阅下面的默认位置中的安装过程中安装的文档︰
`C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES\doc\manual`

作为安装的一部分 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], ，您必须同意 GNU 公共许可条款。 此后，可以运行标准的 R 程序包无需进一步修改，就像在任何其他开源分发为。

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 不修改任何方式中的 R 运行时。 R 运行时执行外部 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 处理并可以独立于运行 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 但是，我们强烈建议您不要运行这些工具时 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 使用 R，若要避免资源争用。

程序与特定的 R 基础程序包分发 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 可以与实例关联的文件夹中找到实例。 例如，如果在默认实例上安装 R Services，R 库位于 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`。

同样，与默认实例相关联的 R 工具将位于 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`,，

有关基本分布的详细信息，请参阅 [安装与 Microsoft R Open 的程序包](https://mran.revolutionanalytics.com/rro/installed/)

### 其他 R 包

除了基本的 R 分布， [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 包含某些专有的 R 包，以及一个框架，用于并行执行的 R、 和支持在远程计算上下文中执行的 R 的库。 

R 功能-R 基分发加上 R 的增强的功能和包-此组合的集称为 **Microsoft R**。如果安装 Microsoft R Server （独立） 时，您将获得一组相同的 SQL Server R 服务 （数据库） 具有但位于不同的文件夹中安装的包。 

Microsoft R 包括用于只要有可能更快地数学处理英特尔数学内核库的分布。 例如，基本线性代数 (BLAS) 库用于许多加载项包也与 R 本身。 有关详细信息，请参阅以下文章︰

+ [Intel 数学内核如何加快 R](http://blog.revolutionanalytics.com/2014/10/revolution-r-open-mkl.html)
+ [链接到多线程的数学库的 R 的性能优势](http://blog.revolutionanalytics.com/2010/06/performance-benefits-of-multithreaded-r.html)

列出了其中一些上述最重要的元素添加到 Microsoft R **RevoScaleR** 和 **RevoPemaR** 包。 这些是更好的性能很大程度上用 C 或 c + + 中编写的 R 包。

+ **RevoScaleR。** 包括各种 Api 进行数据操作和分析。 已优化的 Api 来分析数据集过大而无法放入内存，并执行计算分布在多个核心或处理器。

   RevoScaleR Api 还支持更大可伸缩性使用的数据子集。 换而言之，大多数 RevoScaleR 函数可以执行数据以及使用更新到聚合结果的算法的特定块。 因此 R 解决方案基于 RevoScaleR 函数可以处理大型数据集，并且将不绑定到本地内存。

  RevoScaleR 包还支持。XDF 速度更快的移动和用于分析的数据存储的文件格式。 XDF 格式使用纵栏式存储、 可移植性，并且可以用于加载，然后处理来自各种来源，包括文本、 SPS 或 ODBC 连接的数据。 在本教程中提供了如何使用 XDF 格式的一个示例︰ [数据科学深入了解](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)


+ **RevoPemaR。** PEMA 代表外部内存的并行算法。  **RevoPemaR** 包提供的 Api，可用于开发您自己的并行算法。 有关详细信息，请参阅 [RevoPemaR 入门指南](https://msdn.microsoft.com/microsoft-r/rserver/rserver-pemar-getting-started)。

## 另请参阅
[体系结构概述](../../advanced-analytics/r-services/architecture-overview-sql-server-r-services.md)

[SQL Server 以支持 R 服务中的新组件](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)

[安全性概述](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md)
