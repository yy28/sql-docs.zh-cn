---
title: "OLE DB 提供程序 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 6e0488c3-934d-4976-99dc-65c580dc7a3c
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c95c8bdcf9c4c6d93fc94f8393909cdc758c7c87
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="ole-db-providers-ado"></a>OLE DB 提供程序 (ADO)
OLE DB 定义一组 COM 接口，提供在各种信息源中存储的数据进行统一访问的应用程序。 此方法允许数据源以共享其数据通过支持的 DBMS 功能适合于数据源数量的接口。 按照设计，OLE DB 的高性能体系结构基于其使用灵活的、 基于组件的服务模型。 而不是使规定的数量的应用程序的数据之间的中间层，OLE DB 只需要为所需的许多组件完成特定任务。  
  
 例如，假设用户想要运行查询。 请考虑下列情形：  
  
-   数据驻留在关系数据库当前存在的 ODBC 驱动程序，但没有本机 OLE DB 提供程序： 应用程序使用 ADO 适用于 ODBC，然后加载相应的 ODBC 驱动程序与 OLE DB 提供程序通信。 该驱动程序将传递给 DBMS，检索数据的 SQL 语句。  
  
-   数据驻留在 Microsoft SQL Server 没有本机 OLE DB 提供程序： 应用程序使用 ADO 直接与 OLE DB Provider for Microsoft SQL Server 通信。 没有中介是必需的。  
  
-   数据驻留在 Microsoft Exchange Server，有即的 OLE DB 提供程序，但这不会公开的引擎，过程 SQL 查询： 应用程序使用 ADO 与 OLE DB 访问接口对话适用于 Microsoft Exchange 和 OLE DB 查询处理器将调用若要处理查询的组件。  
  
-   数据驻留在 Microsoft NTFS 文件系统中文档的形式： 通过 Microsoft 索引服务，该服务在文件系统，从而启用有效的内容索引的内容和文档的属性使用本机 OLE DB 提供程序访问数据搜索。  
  
 在所有前面示例中，应用程序可以查询的数据。 与最小组件数满足用户的需求。 在每个情况下，仅在需要时，使用其他组件和调用所需的组件。 使用 OLE DB，可重用和共享组件此按需加载极大地分配给高性能。  
  
 提供程序分为两类： 提供数据和提供服务。 数据提供程序拥有其自己的数据，并以表格形式向你的应用程序公开。 服务提供商对服务进行封装生成和使用数据，并增加在 ADO 应用程序的功能。 此外可以将服务提供商进一步定义为服务组件，必须在与其他服务提供程序或组件一起工作。  
  
 ADO 提供一致、 更高级别接口对各种 OLE DB 提供程序。  
  
 本部分包含以下主题。  
  
-   [数据提供程序](../../../ado/guide/data/data-providers.md)  
  
-   [服务提供商和组件](../../../ado/guide/data/service-providers-and-components.md)
