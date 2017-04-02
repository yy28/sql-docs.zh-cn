---
title: "体系结构概述 (SQL Server R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6c4a4f66-ea3e-4a73-acf2-6c8aeafc94b0
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 9
---
# 体系结构概述 (SQL Server R Services)
本部分提供的体系结构概述 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], ，包括安全性、 在 SQL Server 数据库引擎添加到支持 R 组件和开放源代码 R 脚本运行有 SQL Server 中的互操作性的新组件。


## 目标


体系结构 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 设计为支持的开放源代码 R 语言。 当前用户的 R 应该能够端口他们的 R 代码，并执行它在 T-SQL 中相对较小的修改。

但是，SQL Server R Services 还提供了创新，可提供更高的性能和数据库集成更紧密的 R 语言中，以便更快的数据吞吐量和处理，并降低企业开发 R 解决方案的障碍。 这些创新包括开放源代码和专有由 Microsoft 开发的组件。


与 SQL Server 集成的主要目标是为 R，提供改进的性能和可伸缩性而安全地管理数据。 这一目标，向 SQL Server R Services 提供一个支持集成的 Windows 身份验证和基于密码的 SQL 登录名的多进程基础结构。 

+ [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 提供了 R，以及 ScaleR 包和能够并行运行 R 任务的基本分布。
+ SQL Server 中的新组件提供一个安全、 高性能的框架用来运行外部脚本。
+ R 任务执行超出 SQL Server 进程，来提供安全和更高版本的可管理性。
+ [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 管理 R 的所有进程的安全性。 

为了帮助您优化现有的 R 代码，并充分利用这些改进，本部分中的主题介绍新的体系结构详细信息。 通过了解数据处理和分析由处理 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], ，您可以做出适当的选择，有关如何引入数据、 如何最有效地执行特征工程，以及如何使用结果。
 

## 本节内容
+ [R 互操作性](../../advanced-analytics/r-services/r-interoperability-in-sql-server-r-services.md)
+ [为 R Services SQL Server 中的新组件](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)
+ [安全性概述](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md)

## 另请参阅
[R Services 教程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)
