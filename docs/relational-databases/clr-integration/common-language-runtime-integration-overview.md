---
title: 公共语言运行时 (CLR) 集成概述 |Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
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
ms.openlocfilehash: 69903654faf21a7649ec8b54a269e71a99d559c3
ms.sourcegitcommit: 36c5f28d9fc8d2ddd02deb237937c9968d971926
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66354540"
---
# <a name="common-language-runtime-integration"></a>公共语言运行时集成
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并[Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-index)使您能够实现某些使用作为 SQL Server 的服务器端模块 （过程、 函数中使用本机的公共语言运行时 (CLR) 集成的.Net 语言的功能和触发器）。 CLR 为托管代码提供服务，例如跨语言集成、代码访问安全性、对象生存期管理以及调试和分析支持。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户和应用程序开发人员来说，CLR 集成意味着您现在可以使用任何 .NET Framework 语言（包括 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#）编写存储过程、触发器、用户定义类型、用户定义函数（标量函数和表值函数）以及用户定义的聚合函数。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包括预安装的 .NET Framework 版本 4。  

> [!WARNING]
>  CLR 在 .NET Framework 中使用代码访问安全性 (CAS)（不可再作为安全边界）。 使用 `PERMISSION_SET = SAFE` 创建的 CLR 程序集可以访问外部系统资源、调用非托管代码以及获取 sysadmin 特权。 从 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 开始，引入了名为 `clr strict security` 的 `sp_configure` 选项，以增强 CLR 程序集的安全性。 默认启用 `clr strict security`，并将 `SAFE` 和 `EXTERNAL_ACCESS` 程序集与标记为 `UNSAFE` 的程序集同等对待。 可禁用 `clr strict security` 选项以实现后向兼容性，但不建议这样做。 Microsoft 建议所有程序集都通过证书或非对称密钥进行签名，且该证书或非对称密钥具有已在主数据库中获得 `UNSAFE ASSEMBLY` 权限的相应登录名。 有关详细信息，请参阅 [CLR 严格安全性](../../database-engine/configure-windows/clr-strict-security.md)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员还可以将程序集添加到数据库引擎应信任的程序集列表。 有关详细信息，请参阅 [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md)。

## <a name="when-to-use-clr-modules"></a>何时使用 CLR 模块？

CLR 集成，用户可以实现复杂的功能所提供的.Net Framework 正则表达式，如代码用于访问外部资源 （服务器、 web 服务、 数据库）、 自定义加密，等等。服务器端 CLR 集成的好处包括：
  
-   **更好的编程模型。** .NET Framework 语言在许多方面都比 Transact-SQL 丰富，它为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 开发人员提供了以前没有的构造和功能。 开发人员还可以利用 .NET Framework 库的功能，它提供了大量可用于快速有效地解决编程问题的类。  
  
-   **改进了的安全和安全性。** 托管代码在数据库引擎承载的公共语言运行时环境中运行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 利用这一特点为在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本中提供的扩展存储过程提供更安全更可靠的替代方法。  
  
-   **能够定义数据类型和聚合函数。** 用户定义类型和用户定义聚合是两个新的托管数据库对象，这两个对象扩展了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的存储和查询功能。  
  
-   **通过标准化环境简化了的开发。** [!INCLUDE[msCoName](../../includes/msconame-md.md)]数据库开发集成到将来版本的  Visual Studio .NET 开发环境中。 开发人员在开发和调试数据库对象和脚本时所使用的工具与他们编写中间层或客户端层的 .NET Framework 组件和服务时所使用的工具相同。  
  
-   **为了提高的性能和可伸缩性的潜力。** 在多数情况下，.NET Framework 语言编译和执行模型通过 Transact-SQL 提高性能。  
  
 下表列出了本节的主题。  
  
 [CLR 集成的概述](../../relational-databases/clr-integration/clr-integration-overview.md)  
 说明可使用 CLR 集成生成的对象类型，并介绍使用 CLR 集成生成数据库对象的要求。  
  
 [CLR 集成中的新增功能](../../relational-databases/clr-integration/clr-integration-what-s-new.md)  
 介绍此发行版的新功能。  
  
 [CLR 集成体系结构](https://msdn.microsoft.com/library/05e4b872-3d21-46de-b4d5-739b5f2a0cf9)  
 介绍 CLR 集成的设计目标。  
  
 [启用 CLR 集成](../../relational-databases/clr-integration/clr-integration-enabling.md)  
 介绍如何启用 CLR 集成。  
  
## <a name="see-also"></a>请参阅  
 [安装.NET Framework](https://technet.microsoft.com/library/ms166014\(v=SQL.105\).aspx) ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]仅)   
 [CLR 集成的性能](../../relational-databases/clr-integration/clr-integration-architecture-performance.md)  
  
  
