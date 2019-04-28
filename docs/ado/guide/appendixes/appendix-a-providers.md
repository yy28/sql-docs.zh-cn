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
manager: craigg
ms.openlocfilehash: 14194998e699fa3d16ab50ab488c8d1577660dcc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62719906"
---
# <a name="appendix-a-data-and-service-providers"></a>附录 A：数据和服务提供商
本部分解决了三种类型的提供程序： 数据提供程序、 服务提供程序和服务组件。 提供程序分为两类： 提供数据和提供服务。 一个*数据提供程序*拥有其自己的数据，并以表格形式向你的应用程序公开。 一个*服务提供商*对服务生成和使用数据，并增加 ADO 应用程序中的功能进行封装。 此外可以将服务提供商进一步定义作为*服务组件*，其必须与其他服务提供程序或组件一起工作。

## <a name="data-providers"></a>数据提供程序
 ADO 是功能强大且灵活，因为它可以连接到任意多个不同的数据提供程序，并仍公开了相同的编程模型，而不考虑任何给定的提供程序的特定功能。

 但是，每个数据提供程序是唯一的因为应用程序与 ADO 的交互将略有不同的数据提供程序。 差异通常划分为三个类别之一：

-   中的连接参数[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性。

-   [命令](../../../ado/reference/ado-api/command-object-ado.md)对象使用情况。

-   特定于提供程序[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)行为。

 下面列出了为每个 microsoft 当前可用的数据提供程序的详细信息。

|区域|主题|
|----------|-----------|
|ODBC 数据库|[Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)|
|Microsoft 索引服务|[用于 Microsoft 索引服务的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md)|
|Active Directory 服务|[Microsoft Active Directory 服务的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md)|
|Microsoft Jet 数据库|[OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)|
|Microsoft SQL Server|[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)|
|Oracle 数据库|[Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)|
|Internet 发布|[用于 Internet 发布的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)|
|简单的数据源|[Microsoft OLE DB Simple Provider](../../../ado/guide/appendixes/microsoft-ole-db-simple-provider.md)|

## <a name="provider-specific-dynamic-properties"></a>特定于提供程序的动态属性
 [属性](../../../ado/reference/ado-api/properties-collection-ado.md)的集合[连接](../../../ado/reference/ado-api/connection-object-ado.md)，[命令](../../../ado/reference/ado-api/command-object-ado.md)，以及[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象包括特定的动态属性提供程序。 这些属性为 ADO 支持的内置属性以外的提供程序提供特定功能有关的信息。

 建立连接并创建这些对象之后, 使用[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)方法**属性**要获取特定于提供程序的属性的对象的集合。 请参阅提供程序文档和[OLE DB 程序员指南](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)有关这些动态属性的详细信息。

## <a name="service-providers"></a>服务提供商
 若要使用的服务提供程序，必须提供一个关键字。 此外应注意的与每个服务提供程序关联的特定于提供程序的动态属性。 每个服务提供程序的当前可从 Microsoft 获得列出了特定于提供程序的详细信息：

-   [用于 OLE DB 的 Microsoft 数据整理服务](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)

-   [Microsoft OLE DB 永久性提供程序](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)

-   [Microsoft OLE DB 远程处理提供程序](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)

## <a name="service-components"></a>服务组件
 [用于 OLE DB 游标服务](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)服务组件对数据访问接口的游标支持函数进行了补充。 此外需要使用一个关键字，并具有动态属性。

 有关 OLE DB 提供程序的详细信息，请参阅[Microsoft OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx)。

## <a name="provider-commands"></a>提供程序命令
 每个提供程序列出在这里，如果您的应用程序允许用户输入的 SQL 语句作为提供程序命令，必须始终验证用户输入，并使用具有潜在危险的 SQL 语句，如可能的黑客攻击的特别注意`DROP TABLE t1`，作为用户输入的一部分。

## <a name="see-also"></a>请参阅
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md) [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [用于 Internet 发布的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md) [Microsoft Active Directory 服务的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md) [用于 Microsoft 索引服务的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md) [Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md) [Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) [Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) [Microsoft OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [Refresh 方法 (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)
