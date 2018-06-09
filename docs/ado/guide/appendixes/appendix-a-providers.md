---
title: 附录 a： 提供程序 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- providers [ADO]
- ADO, providers
- service providers [ADO]
- service components [ADO]
ms.assetid: e2581b47-b11e-4e1e-b96c-d39c77c5b48a
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a4cd609a06e0d30e28a451a4308cfec337d47f68
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707505"
---
# <a name="appendix-a-data-and-service-providers"></a>附录 a： 数据和服务提供商
本节介绍三种类型的提供程序： 数据提供程序、 服务提供商和服务组件。 提供程序分为两类： 提供数据和提供服务。 A*数据提供程序*拥有其自己的数据，并以表格形式向你的应用程序公开。 A*服务提供商*通过生成和使用数据，并增加在 ADO 应用程序的功能来封装服务。 服务提供商还可进一步定义作为*服务组件*，哪项必须与其他服务提供程序或组件一起工作。

## <a name="data-providers"></a>数据提供程序
 ADO 是功能强大且灵活，因为它可以连接到任意多个不同的数据提供程序，并且仍然可以公开相同的编程模型，而不考虑任何给定的提供程序的特定功能。

 但是，因为每个数据提供程序是唯一的你的应用程序如何与 ADO 交互将略有不同的数据提供程序。 差异通常分为三个类别之一：

-   中的连接参数[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性。

-   [命令](../../../ado/reference/ado-api/command-object-ado.md)对象使用情况。

-   提供程序特定[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)行为。

 下面列出了为每个 Microsoft 从当前可用的数据提供程序的详细信息。

|区域|主题|
|----------|-----------|
|ODBC 数据库|[Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)|
|Microsoft 索引服务|[Microsoft OLE DB Provider for Microsoft 索引服务](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md)|
|Active Directory 服务|[Microsoft Active Directory 服务的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md)|
|Microsoft Jet 数据库|[Microsoft Jet 的 OLE DB 访问接口](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)|
|Microsoft SQL Server|[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)|
|Oracle 数据库|[适用于 Oracle 的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)|
|Internet 发布|[用于 Internet 发布的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)|
|简单的数据源|[Microsoft OLE DB 简单的提供程序](../../../ado/guide/appendixes/microsoft-ole-db-simple-provider.md)|

## <a name="provider-specific-dynamic-properties"></a>提供程序特定的动态属性
 [属性](../../../ado/reference/ado-api/properties-collection-ado.md)的集合[连接](../../../ado/reference/ado-api/connection-object-ado.md)，[命令](../../../ado/reference/ado-api/command-object-ado.md)，和[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象包括特定的动态属性提供程序。 这些属性向 ADO 支持的内置属性以外的提供程序提供有关特定功能的信息。

 建立连接并创建这些对象之后, 使用[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)方法**属性**要获得的提供程序特定属性的对象的集合。 请参阅提供程序文档和[OLE DB 程序员指南](http://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)有关这些动态属性的详细信息。

## <a name="service-providers"></a>服务提供商
 若要使用的服务提供程序，必须提供一个关键字。 你还应注意与每个服务提供程序关联的特定于提供程序的动态属性。 每个服务提供程序的当前可从 Microsoft 获得列出了特定于提供程序的详细信息：

-   [用于 OLE DB 的 Microsoft 数据整理服务](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)

-   [Microsoft OLE DB 永久性提供程序](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)

-   [Microsoft OLE DB 远程处理提供程序](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)

## <a name="service-components"></a>服务组件
 [OLE DB 的游标服务](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)服务组件进行补充的游标支持函数的数据提供程序。 它还需要使用一个关键字，并具有动态属性。

 有关 OLE DB 提供程序的详细信息，请参阅[Microsoft OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx)。

## <a name="provider-commands"></a>提供程序命令
 每个提供程序列出在这里，如果你的应用程序允许用户输入 SQL 语句作为提供程序命令，您必须始终验证用户输入并使用具有潜在危险的 SQL 语句，如可能的黑客攻击的警惕`DROP TABLE t1`，作为用户输入的一部分。

## <a name="see-also"></a>请参阅
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md) [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [用于 Internet 发布的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md) [Microsoft Active Directory 服务的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md) [Microsoft OLE DB Provider for Microsoft 索引服务](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md) [Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md) [Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) [Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) [Microsoft OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [刷新方法 (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)
