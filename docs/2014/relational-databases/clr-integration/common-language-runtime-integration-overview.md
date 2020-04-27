---
title: 公共语言运行时（CLR）集成概述 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- managed code [SQL Server]
- common language runtime [SQL Server], about CLR integration
- cross-language integration
- integrating CLR [SQL Server]
- .NET Framework [SQL Server], common language runtime
- code access security [CLR integration]
- managed code [SQL Server], CLR integration
ms.assetid: 7be9e644-36a2-48fc-9206-faf59fdff4d7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a7764c6e8e45b56e43e592e70b1c85b8d4744b69
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62919322"
---
# <a name="common-language-runtime-clr-integration-overview"></a>公共语言运行时 (CLR) 集成概述
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]现在提供[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows .NET Framework 的公共语言运行时（CLR）组件集成的功能。 CLR 为托管代码提供服务，例如跨语言集成、代码访问安全性、对象生存期管理以及调试和分析支持。 对于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用户和应用程序开发人员来说，CLR 集成意味着您现在可以使用任何 .NET Framework 语言（包括 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET 和 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#）编写存储过程、触发器、用户定义类型、用户定义函数（标量函数和表值函数）以及用户定义的聚合函数。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 包括预安装的 .NET Framework 版本 4。  
  
 下面列出了这一集成的其中一些主要优点：  
  
-   **更好的编程模型。** .NET Framework 语言在许多方面都比 Transact-SQL 丰富，它为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 开发人员提供了以前没有的构造和功能。 开发人员还可以利用 .NET Framework 库的功能，它提供了大量可用于快速有效地解决编程问题的类。  
  
-   **改进了安全和安全性。** 托管代码在数据库引擎承载的公共语言运行时环境中运行。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 利用这一特点为在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 早期版本中提供的扩展存储过程提供更安全更可靠的替代方法。  
  
-   **能够定义数据类型和聚合函数。** 用户定义类型和用户定义聚合是两个新的托管数据库对象，这两个对象扩展了 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的存储和查询功能。  
  
-   **通过标准化环境简化了开发。** 数据库开发集成到将来版本的  Visual Studio .NET 开发环境中。 开发人员在开发和调试数据库对象和脚本时所使用的工具与他们编写中间层或客户端层的 .NET Framework 组件和服务时所使用的工具相同。  
  
-   **具备改善性能和可伸缩性的潜力。** 在多数情况下，.NET Framework 语言编译和执行模型通过 Transact-SQL 提高性能。  
  
 下表列出了本节的主题。  
  
 [CLR 集成的概述](clr-integration-overview.md)  
 说明可使用 CLR 集成生成的对象类型，并介绍使用 CLR 集成生成数据库对象的要求。  
  
 [CLR 集成中的新增功能](clr-integration-what-s-new.md)  
 介绍此发行版的新功能。  
  
 [CLR 集成体系结构](../../database-engine/dev-guide/architecture-of-clr-integration.md)  
 介绍 CLR 集成的设计目标。  
  
 [启用 CLR 集成](clr-integration-enabling.md)  
 介绍如何启用 CLR 集成。  
  
## <a name="see-also"></a>另请参阅  
 [安装 .NET Framework](https://technet.microsoft.com/library/ms166014\(v=SQL.105\).aspx)   
 [CLR 集成的性能](clr-integration-architecture-performance.md)  
  
  
