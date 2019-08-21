---
title: 使用参数元数据 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: db2c1957-91c6-4989-a07b-9f8be6d2033a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 80ff8cebcc4141e8363c25f83821cb4924e6c46a
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026078"
---
# <a name="using-parameter-metadata"></a>使用参数元数据

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

为了查询 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 对象或 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 对象以了解其所包含的参数，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 实现了 [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md) 类。 该类包含很多以单个值的格式返回信息的字段和方法。

若要创建 SQLServerParameterMetaData 对象, 可以使用 SQLServerPreparedStatement 和 SQLServerCallableStatement 类的[getParameterMetaData](../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md)方法。

在下面的示例中, 将向[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]此函数传递示例数据库的打开连接, 使用 SQLServerCallableStatement 类的 getParameterMetaData 方法返回 SQLServerParameterMetaData 对象, 然后使用各种SQLServerParameterMetaData 对象的方法用于显示有关 Humanresources.uspupdateemployeehireinfo 存储过程中包含的参数的类型和模式的信息。

[!code[JDBC#UsingParamMetaData1](../../connect/jdbc/codesnippet/Java/using-parameter-metadata_1.java)]  

> [!NOTE]  
> 将 SQLServerParameterMetaData 类用于预定义的语句时, 有一些限制。
>
> 使用 Microsoft JDBC Driver 6.0 for SQL Server（或更高版本）：在使用 SQL Server 2008 或 2008 R2 时，JDBC 驱动程序支持 SELECT、DELETE、INSERT 和 UPDATE 语句，前提是这些语句不包含子查询和/或联接  。

在使用 SQL Server 2008 或 2008 R2 时，SQLServerParameterMetaData 类也不支持 MERGE 查询。 对于 SQL Server 2012 和较高版本，支持带有复杂查询的参数元数据。

不支持检索加密列的参数元数据。 使用 Microsoft JDBC Driver 4.1 for SQL Server 或 Microsoft JDBC Driver 4.2 for SQL Server：JDBC 驱动程序支持 SELECT、DELETE、INSERT 和 UPDATE 语句，前提是这些语句不包含子查询和/或联接  。 对于 SQLServerParameterMetaData 类, 也不支持合并查询。
