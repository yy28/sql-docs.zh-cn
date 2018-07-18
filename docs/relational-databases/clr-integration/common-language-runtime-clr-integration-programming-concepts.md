---
title: 公共语言运行时 (CLR) 集成编程概念 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- CLR [SQL Server] See common language runtime [SQL Server]
- Database Engine [SQL Server], .NET Framework
- .NET Framework [SQL Server], Database Engine programming
- common language runtime [SQL Server]
- .NET Framework [SQL Server]
ms.assetid: 951bf851-3e6e-4361-ae6a-2bcd5b837ebd
caps.latest.revision: 59
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: df157328c0718a55dae569503e1e5f6bd424131e
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37357029"
---
# <a name="common-language-runtime-clr-integration-programming-concepts"></a>公共语言运行时 (CLR) 集成编程概念
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 开始，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 集成了用于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 的 .NET Framework 的公共语言运行时 (CLR) 组件。 这意味着现在可以使用任何 .NET Framework 语言（包括 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#）来编写存储过程、触发器、用户定义类型、用户定义函数、用户定义聚合和流式表值函数。  
  
 Microsoft.SqlServer.Server 命名空间包括在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中进行 CLR 编程的核心功能。 但是，有关 Microsoft.SqlServer.Server 命名空间的文档位于 .NET Framework SDK。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书不包括该文档。  
  
> [!IMPORTANT]  
>  默认情况下，.NET Framework 随 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一起安装，但不安装 .NET Framework SDK。 如果未在计算机上安装 SDK，并且未将其包括在联机丛书集中，则本节中指向 SDK 内容的链接无效。 请安装 .NET Framework SDK。 安装后，将 SDK 添加到联机丛书集和内容按照中的说明[安装.NET Framework SDK](http://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx)。  
  
> [!NOTE]  
>  CLR 功能，例如，CLR 用户函数，是*不*支持 Azure SQL 数据库。  
  
 下表列出了本节的主题。  
  
 [公共语言运行时&#40;CLR&#41;集成概述](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)  
 提供 CLR 的简短概述，并说明如何以及为什么在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中使用该技术。 描述使用 CLR 创建数据库对象的好处。  
  
 [程序集（数据库引擎）](../../relational-databases/clr-integration/assemblies-database-engine.md)  
 介绍如何在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中使用程序集来部署用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 公共语言运行时 (CLR) 中驻留的一种托管代码语言（而非 [!INCLUDE[tsql](../../includes/tsql-md.md)]）编写的函数、存储过程、触发器、用户定义聚合和用户定义类型。  
  
 [生成与公共语言运行时的数据库对象&#40;CLR&#41;集成](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)  
 描述可以使用 CLR 生成的对象种类，并说明生成 CLR 数据库对象时所要满足的要求。  
  
 [从 CLR 数据库对象进行数据访问](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
 描述 CLR 例程如何访问存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中的数据。  
  
 [CLR 集成安全性](../../relational-databases/clr-integration/security/clr-integration-security.md)  
 描述 CLR 集成安全模型。  
  
 [调试 CLR 数据库对象](../../relational-databases/clr-integration/debugging-clr-database-objects.md)  
 描述调试 CLR 数据库对象的限制和要求。  
  
 [部署 CLR 数据库对象](../../relational-databases/clr-integration/deploying-clr-database-objects.md)  
 描述如何将程序集部署到生产服务器。  
  
 [管理 CLR 集成程序集](../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)  
 描述如何创建和删除 CLR 集成程序集。  
  
 [托管数据库对象监视和故障排除](../../relational-databases/clr-integration/monitoring-and-troubleshooting-managed-database-objects.md)  
 介绍用于对在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中运行的托管数据库对象和程序集进行监视和故障排除的工具的相关信息。  
  
 [公共语言运行时 (CLR) 集成的使用方案和示例](http://msdn.microsoft.com/library/33aac25f-abb4-4f29-af88-4a0dacd80ae7)  
 描述使用 CLR 对象的应用场景和代码示例。  
  
## <a name="see-also"></a>请参阅  
 [程序集&#40;数据库引擎&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [安装.NET Framework SDK](http://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx)  
  
  
