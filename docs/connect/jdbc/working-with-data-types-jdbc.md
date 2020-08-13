---
title: 处理数据类型 (JDBC)
description: 了解如何通过这些示例应用程序在 SQL Server 的 JDBC 驱动程序中处理数据类型。
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b39f44d0-3710-4bc6-880c-35bd8c10a734
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6994e7ce587cf72d7879c79604cbe3c68873ddf0
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923275"
---
# <a name="working-with-data-types-jdbc"></a>处理数据类型 (JDBC)

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 的主要功能是允许 Java 开发人员访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中包含的数据。 为了实现此功能，JDBC 驱动程序充当了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型和 Java 语言类型以及对象之间的转换中介。

> [!NOTE]
> 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 JDBC 驱动程序数据类型的详细说明（包括它们的区别以及如何将它们转换为 Java 语言数据类型），请参阅[了解 JDBC 驱动程序数据类型](understanding-the-jdbc-driver-data-types.md)。

为了使用 SQL Server 数据类型，JDBC 驱动程序为 [SQLServerPreparedStatement](reference/sqlserverpreparedstatement-class.md) 和 [SQLServerCallableStatement](reference/sqlservercallablestatement-class.md) 类提供了 get\<Type> 和 set\<Type> 方法，为 [SQLServerResultSet](reference/sqlserverresultset-class.md) 类提供了 get\<Type> 和 update\<Type> 方法。 要使用哪个方法取决于所使用的数据类型以及是否要使用结果集和查询。

此部分的主题说明了如何在 Java 应用程序中使用 JDBC 驱动程序数据类型来访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据。

## <a name="in-this-section"></a>在本节中

|主题|说明|
|-----------|-----------------|
|[基本数据类型示例](basic-data-types-sample.md)|说明如何使用结果集的 getter 方法来检索基本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型值，以及如何使用结果集的 update 方法来更新这些值。|
|[SQLXML 数据类型示例](sqlxml-data-type-sample.md)|说明如何在关系数据库中存储 XML 数据，如何从数据库中检索 XML 数据，以及如何使用 SQLXML Java 数据类型分析 XML 数据  。|
|[空间数据类型示例](spatial-data-types-sample.md)|描述如何使用 Microsoft JDBC 驱动程序定义的 Geometry**** 和 Geography**** Java 类型来存储和检索 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中空间数据类型“Geometry”和“Geography”的数据。|

## <a name="see-also"></a>另请参阅

[示例 JDBC 驱动程序应用程序](sample-jdbc-driver-applications.md)
