---
title: 使用数据类型 (JDBC) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b39f44d0-3710-4bc6-880c-35bd8c10a734
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6af72a4e9157de72a46ecbb7443c0f58d3b400d7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003849"
---
# <a name="working-with-data-types-jdbc"></a>使用数据类型 (JDBC)

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 的主要功能是允许 Java 开发人员访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中包含的数据。 为了实现此功能，JDBC 驱动程序充当了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型和 Java 语言类型以及对象之间的转换中介。  
  
> [!NOTE]  
> 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 JDBC 驱动程序数据类型（包括它们之间的差异以及如何将其转换到 Java 语言数据类型）的详细说明，请参阅[了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)。  
  
为了使用 SQL Server 数据类型，JDBC 驱动程序为 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 和 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 类提供了 get\<Type> 和 set\<Type> 方法，为 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 类提供了 get\<Type> 和 update\<Type> 方法。 要使用哪个方法取决于所使用的数据类型以及是否要使用结果集和查询。  
  
此部分的主题说明了如何在 Java 应用程序中使用 JDBC 驱动程序数据类型来访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|描述|  
|-----------|-----------------|  
|[基本数据类型示例](../../connect/jdbc/basic-data-types-sample.md)|说明如何使用结果集的 getter 方法来检索基本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型值，以及如何使用结果集的 update 方法来更新这些值。|  
|[SQLXML 数据类型示例](../../connect/jdbc/sqlxml-data-type-sample.md)|说明如何在关系数据库中存储 XML 数据，如何从数据库中检索 XML 数据，以及如何使用 SQLXML Java 数据类型分析 XML 数据  。|  
|[空间数据类型示例](../../connect/jdbc/spatial-data-types-sample.md)|介绍如何使用由 Microsoft JDBC Driver 定义的**Geometry**和**Geography** Java 类型存储和检索具有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]空间数据类型 "geometry" 和 "地域" 的数据。|

## <a name="see-also"></a>另请参阅

[示例 JDBC 驱动程序应用程序](../../connect/jdbc/sample-jdbc-driver-applications.md)  
