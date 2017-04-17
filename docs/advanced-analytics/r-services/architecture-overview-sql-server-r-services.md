---
title: "体系结构概述 (SQL Server R Services) | Microsoft Docs"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6c4a4f66-ea3e-4a73-acf2-6c8aeafc94b0
caps.latest.revision: 9
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9f334b74e34acecc97b95e2b5b7052eda15585cf
ms.lasthandoff: 04/11/2017

---
# <a name="architecture-overview-sql-server-r-services"></a>体系结构概述 (SQL Server R Services)
本部分概述了 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 的体系结构，包括安全性、SQL Server 数据库引擎中添加的用于支持 R 组件的新组件，以及 SQL Server 中运行的开放源代码 R 脚本的互操作性。


## <a name="goals"></a>目标


[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 的体系结构旨在支持开放源代码 R 语言。 R 的当前用户应该能够通过相对较小的修改移植其 R 代码，并在 T-SQL 中执行。

但是，SQL Server R Services 还提供了这样的创新：可提供更高的性能和 R 语言的更紧密数据库集成，以实现更快的数据吞吐量和处理，并减少企业开发 R 解决方案的障碍。 这些创新包括开放源代码和由 Microsoft 开发的专用组件。


与 SQL Server 集成的主要目标是为 R 提供改进的性能和可伸缩性，同时安全地管理数据。 为实现这一目标，SQL Server R Services 提供了一个多进程基础结构，以同时支持集成 Windows 身份验证和基于密码的 SQL 登录。 

+ [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 提供了 R 以及 ScaleR 包的基本分发，并能够并行运行 R 任务。
+ SQL Server 中的新组件提供一个安全、高性能的框架，用于运行外部脚本。
+ R 任务在 SQL Server 进程外执行，以提供安全性和更好的可管理性。
+ [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 管理所有 R 进程的安全性。 

为了帮助你优化现有 R 代码并充分利用这些改进，本部分中的主题详细介绍了这一新体系结构。 了解 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 如何进行数据处理和分析后，你便可以对于如何引入数据、如何最有效地执行特征工程以及如何使用结果做出适当的选择。
 

## <a name="in-this-section"></a>本节内容
+ [R 互操作性](../../advanced-analytics/r-services/r-interoperability-in-sql-server-r-services.md)
+ [SQL Server 中适用于 R Services 的新组件](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)
+ [安全性概述](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md)

## <a name="see-also"></a>另请参阅
[R Services 教程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)


