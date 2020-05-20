---
title: Microsoft ActiveX 数据对象（ADO） |Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, about
ms.assetid: 2fa6237b-44b8-4b6c-9952-5acd80a54e20
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18b9a6590ce777402456c8e9f8c8f28807ec5670
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606609"
---
# <a name="microsoft-activex-data-objects-ado"></a>Microsoft ActiveX 数据对象 (ADO)

ActiveX 数据对象是一种编程模型，这意味着它不依赖于任何给定的后端引擎。 然而，当前支持 ADO 模型的引擎是 OLE DB。 有很多本机 OLE DB 提供程序和用于 ODBC 的 OLE DB 访问接口。 ADO 用于 c + + 和 Visual Basic 程序连接到 SQL Server 和其他数据库。 当然，它还适用于连接到云中的 Azure SQL 数据库。

本文的每个部分都介绍了 ADO 的组成部分。

> [!NOTE]
> ADO.NET 不同于 ADO。 ADO.NET 和许多其他 SQL 连接驱动程序及其语言从[SQL Server 驱动程序](../connect/sql-connection-libraries.md)开始讨论。

  
## <a name="ado"></a>ADO  
 Microsoft ActiveX 数据对象（ADO）允许客户端应用程序通过 OLE DB 提供程序访问和处理来自各种源的数据。 它的主要优点是易于使用、高速、低内存开销和较小的磁盘空间。 ADO 支持用于生成客户端/服务器和基于 Web 的应用程序的关键功能。  
  
## <a name="ado-md"></a>ADO MD  
 Microsoft ActiveX 数据对象(多维) （ADO MD）可让你轻松地从 Microsoft Visual Basic 和 Microsoft Visual C++ 等语言访问多维数据。 ADO MD 扩展 Microsoft ActiveX 数据对象（ADO）以包括特定于多维数据的对象，例如 CubeDef 和单元集对象。 使用 ADO MD 可以浏览多维架构、查询多维数据集和检索结果。  
  
 与 ADO 一样，ADO MD 使用底层 OLE DB 提供程序来获取对数据的访问权限。 若要使用 ADO MD，提供程序必须是由 OLAP 规范的 OLE DB 定义的多维数据提供程序（MDP）。 MDPs 在多维视图中呈现数据，而不是在表格视图中显示数据的表格数据提供程序（TDPs）。 有关提供程序支持的特定语法和行为的详细信息，请参阅 OLAP OLE DB 提供程序的文档。  
  
## <a name="rds"></a>RDS  
 远程数据服务（RDS）是 ADO 的一项功能，您可以使用它将数据从服务器移到客户端应用程序或网页，操作客户端上的数据，并在一次往返中将更新返回到服务器。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="adox"></a>ADOX  
 用于数据定义语言和安全（ADOX）的 Microsoft ActiveX 数据对象扩展是 ADO 对象和编程模型的扩展。 ADOX 包含用于创建和修改架构以及安全性的对象。 由于它是一种基于对象的架构处理方法，因此你可以编写代码来处理各种数据源，而不考虑它们的本机语法差异。  
  
 ADOX 是核心 ADO 对象的配套库。 它公开了用于创建、修改和删除架构对象（如表和过程）的其他对象。 它还包括安全对象以维护用户和组以及授予和撤消对对象的权限。  
  
## <a name="documentation"></a>文档  
 [ADO 安全设计问题](../ado/guide/ado-security-design-issues.md)  
  
 [ADO 程序员指南](../ado/guide/ado-programmer-s-guide.md)  
  
 介绍如何使用 ADO、RDS、ADO MD 和 ADOX。  
  
 [ADO 程序员参考](../ado/reference/ado-programmer-s-reference.md)  
  
 ADO 文档的本节内容包含每个 ADO、RDS、ADO MD 和 ADOX 对象、集合、属性、动态属性、方法、事件和枚举的相关主题。  
  
 [ADO 术语表](../ado/ado-glossary.md)  
  
## <a name="support"></a>支持  
 有关 ADO 问题的免费帮助，请尝试发布到 ADO 公共新闻组。 此新闻组由涉及 ADO 的 Microsoft 产品支持服务（PSS）支持专业人员以及其他有经验的 ADO 开发人员进行监视。  
  
 有关支持选项的更多信息，请访问 Microsoft 帮助和支持网站。


