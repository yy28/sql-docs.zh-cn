---
title: 公共语言运行时 (CLR) 集成编程概念 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- CLR [SQL Server] See common language runtime [SQL Server]
- Database Engine [SQL Server], .NET Framework
- .NET Framework [SQL Server], Database Engine programming
- common language runtime [SQL Server]
- .NET Framework [SQL Server]
ms.assetid: 951bf851-3e6e-4361-ae6a-2bcd5b837ebd
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ffd706cdb17bd73281ee4a62842362b09c6311ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62922551"
---
# <a name="common-language-runtime-clr-integration-programming-concepts"></a>公共语言运行时 (CLR) 集成编程概念
  从 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 开始，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 集成了用于 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 的 .NET Framework 的公共语言运行时 (CLR) 组件。 这意味着现在可以使用任何 .NET Framework 语言（包括 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET 和 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#）来编写存储过程、触发器、用户定义类型、用户定义函数、用户定义聚合和流式表值函数。  
  
 Microsoft.SqlServer.Server 命名空间包括在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中进行 CLR 编程的核心功能。 但是，有关 Microsoft.SqlServer.Server 命名空间的文档位于 .NET Framework SDK。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 联机丛书不包括该文档。  
  
> [!IMPORTANT]  
>  默认情况下，.NET Framework 随 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 一起安装，但不安装 .NET Framework SDK。 如果未在计算机上安装 SDK，并且未将其包括在联机丛书集中，则本节中指向 SDK 内容的链接无效。 请安装 .NET Framework SDK。 安装后，将 SDK 添加到联机丛书集和内容按照中的说明[安装.NET Framework SDK](https://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx)。  
  
 下表列出了本节的主题。  
  
 [公共语言运行时&#40;CLR&#41;集成概述](common-language-runtime-integration-overview.md)  
 提供 CLR 的简短概述，并说明如何以及为什么在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中使用该技术。 描述使用 CLR 创建数据库对象的好处。  
  
 [程序集（数据库引擎）](assemblies-database-engine.md)  
 介绍如何在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中使用程序集来部署用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 公共语言运行时 (CLR) 中驻留的一种托管代码语言（而非 [!INCLUDE[tsql](../../../includes/tsql-md.md)]）编写的函数、存储过程、触发器、用户定义聚合和用户定义类型。  
  
 [生成与公共语言运行时的数据库对象&#40;CLR&#41;集成](database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)  
 描述可以使用 CLR 生成的对象种类，并说明生成 CLR 数据库对象时所要满足的要求。  
  
 [从 CLR 数据库对象进行数据访问](data-access/data-access-from-clr-database-objects.md)  
 描述 CLR 例程如何访问存储在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例中的数据。  
  
 [CLR 集成安全性](security/clr-integration-security.md)  
 描述 CLR 集成安全模型。  
  
 [调试 CLR 数据库对象](debugging-clr-database-objects.md)  
 描述调试 CLR 数据库对象的限制和要求。  
  
 [部署 CLR 数据库对象](deploying-clr-database-objects.md)  
 描述如何将程序集部署到生产服务器。  
  
 [管理 CLR 集成程序集](assemblies/managing-clr-integration-assemblies.md)  
 描述如何创建和删除 CLR 集成程序集。  
  
 [托管数据库对象监视和故障排除](monitoring-and-troubleshooting-managed-database-objects.md)  
 介绍用于对在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中运行的托管数据库对象和程序集进行监视和故障排除的工具的相关信息。  
  
 [公共语言运行时 (CLR) 集成的使用方案和示例](../../database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
 描述使用 CLR 对象的应用场景和代码示例。  
  
## <a name="see-also"></a>请参阅  
 [程序集&#40;数据库引擎&#41;](assemblies-database-engine.md)   
 [安装.NET Framework SDK](https://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx)  
  
  
