---
title: "Microsoft ActiveX 数据对象 (ADO) |Microsoft 文档"
ms.custom: 
ms.date: 07/25/2017
ms.reviewer: 
ms.suite: 
ms.prod: sql-non-specified
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO, about
ms.assetid: 2fa6237b-44b8-4b6c-9952-5acd80a54e20
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 28fa2c279cfd7964d8516514a3caed129e335692
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-activex-data-objects-ado"></a>Microsoft ActiveX 数据对象 (ADO)

在 c + + 程序中使用 ADO 连接到 SQL Server。 当然，它还可用于连接到在云中的 Azure SQL 数据库。

这篇文章中的每个部分介绍 ADO 的一个组件。

> [!NOTE]
> ADO.NET 是不同于 ADO。 ADO.NET 和许多其他 SQL 连接驱动程序和其语言开始讨论[SQL Server 驱动程序](../connect/sql-connection-libraries.md)。

  
## <a name="ado"></a>ADO  
 Microsoft ActiveX 数据对象 (ADO) 启用客户端应用程序，以访问和处理从各种源通过 OLE DB 访问接口的数据。 它的主要优点是易于使用、 高速、 低内存开销和小磁盘空间占用量。 ADO 支持用于生成客户端/服务器和基于 Web 的应用程序的主要功能。  
  
## <a name="ado-md"></a>ADO MD  
 通过 Microsoft Visual Basic 中，和 Microsoft Visual c + + 等语言情况下，Microsoft ActiveX 数据对象 （多维） (ADO MD) 提供对多维数据的轻松访问。 ADO MD 扩展 Microsoft ActiveX 数据对象 (ADO) 以包括特定于多维数据，例如 CubeDef 和单元集的对象的对象。 使用 ADO MD 中，您可以浏览多维架构、 查询多维数据集，并检索结果。  
  
 ADO，如 ADO MD 使用基础的 OLE DB 提供程序对数据进行访问。 若要使用 ADO MD，提供程序必须是多维数据提供程序 (MDP)，因为 OLE DB for OLAP 规范所定义。 Mdp 表格视图中呈现而不是表格数据提供程序 (Tdp) 的多维视图中的数据显示数据。 请参阅有关特定语法和行为你提供程序支持的更多详细信息的 OLAP OLE DB 提供程序的文档。  
  
## <a name="rds"></a>RDS  
 远程数据服务 (RDS) 是一项功能的 ADO，这可以用于将数据从一台服务器移到客户端应用程序或网页，操作客户端上的数据并返回到单个往返过程中的服务器的更新。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="adox"></a>ADOX  
 Microsoft ActiveX 数据对象扩展数据定义语言和安全 (ADOX) 是 ADO 对象和编程模型的扩展。 ADOX 包括架构创建和修改，以及安全的对象。 因为它是架构操作的基于对象的方法，你可以编写代码来处理各种数据源而不考虑其本机语法方面的差异。  
  
 ADOX 是对核心 ADO 对象的助理库。 它公开用于创建、 修改和删除架构对象，如表和过程的其他对象。 它还包括安全对象维护用户和组并将 grant 和 revoke 对象权限。  
  
## <a name="documentation"></a>文档  
 [ADO 安全设计问题](../ado/guide/ado-security-design-issues.md)  
  
 [ADO 程序员指南](../ado/guide/ado-programmer-s-guide.md)  
  
 使用 ADO、 RDS、 ADO MD 和 ADOX 简介。  
  
 [ADO 程序员参考](../ado/reference/ado-programmer-s-reference.md)  
  
 ADO 文档的此部分包含有关每个 ADO、 RDS、 ADO MD 和 ADOX 对象、 集合、 属性、 动态属性、 方法、 事件和枚举的主题。  
  
 [ADO 术语表](../ado/ado-glossary.md)  
  
## <a name="support"></a>支持  
 免费帮助的 ADO 问题，请尝试发布到 ADO 公共新闻组。 通过 Microsoft 产品支持服务 (PSS) 支持专业人员介绍 ADO，以及其他经验丰富的 ADO 开发人员，将监视此新闻组。  
  
 可以在 Microsoft 帮助和支持网站上找到有关支持选项的详细信息。



