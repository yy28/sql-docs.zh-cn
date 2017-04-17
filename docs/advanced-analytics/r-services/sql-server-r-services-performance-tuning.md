---
title: "SQL Server R Services 性能优化 | Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf6f3b7d-f9f9-4e45-b0d1-07850b53e0c5
caps.latest.revision: 20
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d0b171254b4c4ed07ae946ac01fbbb3fbc743df6
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-r-services-performance-tuning"></a>SQL Server R Services 性能优化
[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 提供了一个平台用于开发可发掘新见解的智能应用程序。 数据科学家可以利用 R 语言的强大功能，使用 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中存储的数据来训练和创建模型。 模型可用于生产后，数据科学家就可以与数据库管理员和 SQL 工程师协作在生产环境中部署其解决方案。 此部分中的信息针对有关在创建和训练模型时，以及将模型部署到生产环境时如何优化性能，提供高级指导。

本文档中的信息假定你熟悉 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 概念和术语。 有关 R Services 的一般信息，请参阅 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)。

> [!NOTE]
> 虽然本部分中的很多信息是针对配置 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 的一般指南，但是有些信息特定于 RevoScaleR 分析函数。

## <a name="in-this-section"></a>本节内容

* [SQL Server 配置](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)：此文档提供有关如何配置安装 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 的硬件的指导。 它最适用于__数据库管理员__。

* [R 和数据优化](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)：此文档提供有关如何将 R 脚本与 R Services 配合使用的指导。 它最适用于__数据科学家__。

* [性能案例研究](../../advanced-analytics/r-services/performance-case-study-r-services.md)：此文档提供测试数据和 R 脚本，可用于测试在以前的文档中提供的指导的作用。

## <a name="references"></a>References

以下是在本文档的开发中使用的信息的链接。

* [如何确定 64 位版本 Windows 的合适页面文件大小](https://support.microsoft.com/kb/2860880)

* [数据压缩](../../relational-databases/data-compression/data-compression.md)

* [对表或索引启用压缩功能](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

* [对表或索引禁用压缩功能](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

* [DISKSPD 存储负载生成器/性能测试工具](https://github.com/microsoft/diskspd)

* [FSUtil 实用工具参考](https://technet.microsoft.com/library/cc753059.aspx)

* [重新组织和重新生成索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

* [R Services](../../advanced-analytics/r-services/r-services.md)

* [rxDForest 和 rxDTree 的性能优化选项](https://support.microsoft.com/kb/3104235)

* [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)

* [在 25 个函数中探索 R 和 ScaleR](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started-tutorial)

* [资源调控器](../../relational-databases/resource-governor/resource-governor.md)

## <a name="see-also"></a>另请参阅

 
 [适用于 R Services 的 SQL Server 配置](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [性能案例研究](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 
 [R 和数据优化](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)

