---
title: Microsoft ActiveX 数据对象 (ADO) |Microsoft Docs
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
ms.openlocfilehash: 0ca9c22cb54c54441f848ecbf367e92e30c1fd83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921871"
---
# <a name="microsoft-activex-data-objects-ado"></a>Microsoft ActiveX 数据对象 (ADO)

ADO 中使用C++程序连接到 SQL Server。 当然，它也适用于连接到在云中的 Azure SQL 数据库。

这篇文章中的每个部分介绍了 ADO 的组件。

> [!NOTE]
> ADO.NET 是不同于 ADO。 ADO.NET 和许多其他 SQL 连接驱动程序和其语言开始讨论[SQL Server 驱动程序](../connect/sql-connection-libraries.md)。

  
## <a name="ado"></a>ADO  
 Microsoft ActiveX 数据对象 (ADO) 启用客户端应用程序访问和处理从各种源通过 OLE DB 访问接口的数据。 它的主要优点是易于使用、 高速度、 低内存开销和小磁盘空间占用量。 ADO 支持构建客户端/服务器和基于 Web 的应用程序的主要功能。  
  
## <a name="ado-md"></a>ADO MD  
 Microsoft ActiveX 数据对象 （多维） (ADO MD) 可轻松访问多维数据从 Microsoft Visual Basic 和 Microsoft Visual 等语言C++。 ADO MD 扩展了 Microsoft ActiveX 数据对象 (ADO) 以包括特定于多维数据，例如 CubeDef 和单元集对象的对象。 使用 ADO MD 可以浏览多维架构、 查询多维数据集，并检索结果。  
  
 例如 ADO，ADO MD 使用基础的 OLE DB 访问接口来访问数据。 若要使用 ADO MD，提供程序必须按照 OLE DB for OLAP 规范的定义是多维数据提供程序 (MDP)。 Mdp 表格视图中呈现数据而不是表格数据提供程序 (Tdp) 的多维视图中显示数据。 请参阅更多详细信息的特定语法和支持您的提供程序的行为在 OLAP OLE DB 提供程序的文档。  
  
## <a name="rds"></a>RDS  
 远程数据服务 (RDS) 是一项功能的 ADO 中，通过它将数据从一台服务器移到客户端应用程序或网页、 操作在客户端上的数据并且将更新返回单个往返过程中的服务器。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="adox"></a>ADOX  
 数据定义语言和安全 (ADOX) 的 Microsoft ActiveX 数据对象扩展插件是 ADO 对象和编程模型的扩展。 ADOX 包括架构创建和修改，以及安全的对象。 因为它是基于对象的架构操作方法，您可以编写代码来处理各种数据源而不考虑其本机语法之间的差异。  
  
 ADOX 是伴随库到核心 ADO 对象。 它公开用于创建、 修改和删除架构对象，如表和过程的其他对象。 它还包括安全对象来维护用户和组，并以授予和撤消对对象的权限。  
  
## <a name="documentation"></a>文档  
 [ADO 安全设计问题](../ado/guide/ado-security-design-issues.md)  
  
 [ADO 程序员指南](../ado/guide/ado-programmer-s-guide.md)  
  
 使用 ADO、 RDS、 ADO MD 和 ADOX 的简介。  
  
 [ADO 程序员参考](../ado/reference/ado-programmer-s-reference.md)  
  
 ADO 文档的此部分包含每个 ADO、 RDS、 ADO MD 和 ADOX 对象、 集合、 属性、 动态属性、 方法、 事件和枚举的主题。  
  
 [ADO 术语表](../ado/ado-glossary.md)  
  
## <a name="support"></a>支持  
 免费帮助解决 ADO 的问题，请尝试发布到 ADO 公共新闻组。 此新闻组进行监视的 Microsoft 产品支持服务 (PSS) 支持专业人员介绍 ADO，和其他有经验的 ADO 开发人员。  
  
 可以在 Microsoft 帮助和支持网站上找到有关支持选项的进一步信息。


