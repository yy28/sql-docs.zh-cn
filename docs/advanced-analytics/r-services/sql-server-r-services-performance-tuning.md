---
title: "SQL Server R Services 性能优化 | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cf6f3b7d-f9f9-4e45-b0d1-07850b53e0c5
caps.latest.revision: 20
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 19
---
# SQL Server R Services 性能优化
[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 提供了一个平台用于开发可发掘新见解的智能应用程序。 数据科学家可以使用 R 语言的强大功能来训练并创建使用数据存储在模型 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 该模型用于生产准备就绪后，数据科学家可以使用数据库管理员和 SQL 工程师部署在生产中的其解决方案。 此部分中的信息提供有关优化性能，包括时创建并定型模型，并将模型部署到生产环境时高级别的指南。

本文档中的信息假定您熟悉 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 概念和术语。 R 服务的一般信息，请参阅 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)。

> [!NOTE]
> 很多本部分中的信息时的配置的一般指南 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], ，某些信息是特定于 RevoScaleR 分析函数。

## 本节内容

* [SQL Server 配置](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)︰ 本文档提供配置硬件指南， [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 上安装。 它是对最有用 __数据库管理员__。

* [R 和数据优化](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)︰ 本文档提供在 R 脚本中使用 R 服务的指导。 它是对最有用 __数据科学家__。

* [性能案例研究](../../advanced-analytics/r-services/performance-case-study-r-services.md)︰ 本文档提供测试数据和可用于测试在之前的文档中提供指南的影响的 R 脚本。

## References

以下是本文档的开发中使用的信息的链接。

* [如何确定 64 位版本的 Windows 的合适的页面文件大小](https://support.microsoft.com/kb/2860880)

* [数据压缩](../../relational-databases/data-compression/data-compression.md)

* [对表或索引启用压缩功能](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

* [对表或索引禁用压缩功能](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

* [DISKSPD 存储负载生成器/性能测试工具](https://github.com/microsoft/diskspd)

* [FSUtil 实用程序引用](https://technet.microsoft.com/library/cc753059.aspx)

* [重新组织和重新生成索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

* [R Services](../../advanced-analytics/r-services/r-services.md)

* [RxDForest 和 rxDTree 性能优化选项](https://support.microsoft.com/kb/3104235)

* [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)

* [RevoScaleR 用户指南](https://packages.revolutionanalytics.com/doc/7.0.0/win/RevoScaleR_Users_Guide.pdf)

* [资源调控器](../../relational-databases/resource-governor/resource-governor.md)

## 另请参阅

 
 [R 服务的 SQL Server 配置](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [性能案例研究](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 
 [R 和数据优化](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)