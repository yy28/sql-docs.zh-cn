---
title: 附录 A：提供程序 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- providers [ADO]
- ADO, providers
- service providers [ADO]
- service components [ADO]
ms.assetid: e2581b47-b11e-4e1e-b96c-d39c77c5b48a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4ffecfc87ec23fc4d62174dae31220511c9f72d4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926971"
---
# <a name="appendix-a-data-and-service-providers"></a>附录 A：数据和服务提供商
本节介绍三种类型的提供程序：数据提供程序、服务提供程序和服务组件。 提供程序分为两类：提供数据的提供程序和提供服务的提供程序。 *数据访问接口*拥有自己的数据，并以表格形式向应用程序公开该数据。 *服务提供程序*通过生成和使用数据并在 ADO 应用程序中扩充功能来封装服务。 服务提供商还可以被进一步定义为*服务组件*，该组件必须与其他服务提供商或组件一起工作。

## <a name="data-providers"></a>数据提供程序
 ADO 的功能强大且灵活，因为它可以连接到多个不同的数据访问接口中的任何一种，并且仍公开相同的编程模型，而与任何给定提供程序的特定功能无关。

 但是，由于每个数据提供程序都是唯一的，因此，应用程序与 ADO 交互的方式将与数据访问接口略有不同。 这些差异通常分为以下三个类别之一：

-   [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性中的连接参数。

-   [命令](../../../ado/reference/ado-api/command-object-ado.md)对象的用法。

-   特定于提供程序的[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)行为。

 下面列出了 Microsoft 当前提供的每个数据提供程序的详细信息。

|区域|主题|
|----------|-----------|
|ODBC 数据库|[Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)|
|Microsoft 索引服务|[Microsoft OLE DB Provider for Microsoft Indexing Service](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md)|
|Active Directory 服务|[Microsoft OLE DB Provider for Microsoft Active Directory 服务](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md)|
|Microsoft Jet 数据库|[用于 Microsoft Jet 的 OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)|
|Microsoft SQL Server|[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)|
|Oracle 数据库|[Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)|
|Internet 发布|[用于 Internet 发布的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)|
|简单数据源|[Microsoft OLE DB 简单提供程序](../../../ado/guide/appendixes/microsoft-ole-db-simple-provider.md)|

## <a name="provider-specific-dynamic-properties"></a>特定于提供程序的动态属性
 [连接](../../../ado/reference/ado-api/connection-object-ado.md)、[命令](../../../ado/reference/ado-api/command-object-ado.md)和[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象的[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合包括特定于提供程序的动态属性。 这些属性提供了有关特定于提供程序的功能的信息，这些功能超出了 ADO 支持的内置属性。

 建立连接并创建这些对象后，请使用对象的**Properties**集合上的[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法来获取特定于提供程序的属性。 有关这些动态属性的详细信息，请参阅提供程序文档和[OLE DB 程序员指南](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)。

## <a name="service-providers"></a>服务提供商
 若要使用服务提供程序，必须提供关键字。 还应注意与每个服务提供程序相关联的特定于提供程序的动态属性。 为当前提供的每个服务提供商列出了特定于提供程序的详细信息：

-   [用于 OLE DB 的 Microsoft 数据整理服务](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)

-   [Microsoft OLE DB 永久性提供程序](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)

-   [Microsoft OLE DB 远程处理提供程序](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)

## <a name="service-components"></a>服务组件
 OLE DB 服务组件的[游标服务](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)对数据提供程序的游标支持函数进行了补充。 它还需要关键字并且具有动态属性。

 有关 OLE DB 提供程序的详细信息，请参阅[Microsoft OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx)。

## <a name="provider-commands"></a>提供程序命令
 对于此处列出的每个提供程序，如果你的应用程序允许用户输入 SQL 语句作为提供程序命令，则必须始终验证用户输入，并使用潜在的危险 SQL 语句（如`DROP TABLE t1`）作为用户输入的一部分来警惕可能的黑客攻击。

## <a name="see-also"></a>另请参阅
 [用于 Internet 发布的 microsoft OLE DB 提供程序的](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)[命令对象（Ado）](../../../ado/reference/ado-api/command-object-ado.md) [连接对象（ado）](../../../ado/reference/ado-api/connection-object-ado.md) Microsoft [OLE DB Provider for microsoft Active Directory Service](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md) [Microsoft OLE DB PROVIDER for microsoft 索引服务](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md)microsoft [OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md) [Oracle 的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) [microsoft OLE DB](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) provider FOR microsoft [Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) [Properties Collection （ado](../../../ado/reference/ado-api/properties-collection-ado.md) ） [Recordset 对象（ado）](../../../ado/reference/ado-api/recordset-object-ado.md) [Refresh 方法（RDS）](../../../ado/reference/rds-api/refresh-method-rds.md)
