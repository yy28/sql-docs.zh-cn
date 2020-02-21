---
title: 使用参数元数据 | Microsoft Docs
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
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "69026078"
---
# <a name="using-parameter-metadata"></a>使用参数元数据

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

为了查询 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 对象或 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 对象以了解其所包含的参数，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 实现了 [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md) 类。 该类包含很多以单个值的格式返回信息的字段和方法。

若要创建 SQLServerParameterMetaData 对象，可以使用 SQLServerPreparedStatement 类和 SQLServerCallableStatement 类的 [getParameterMetaData](../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md) 方法。

在以下示例中，[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库的打开连接传递给函数，SQLServerCallableStatement 类的 getParameterMetaData 方法用于返回 SQLServerParameterMetaData 对象，然后使用 SQLServerParameterMetaData 对象的各种方法显示有关 HumanResources.uspUpdateEmployeeHireInfo 存储过程内所含参数的类型和模式的信息。

[!code[JDBC#UsingParamMetaData1](../../connect/jdbc/codesnippet/Java/using-parameter-metadata_1.java)]  

> [!NOTE]  
> 将 SQLServerParameterMetaData 类和预定义语句一起使用时，存在一些限制。
>
> **对于 Microsoft JDBC Driver 6.0 for SQL Server（或更高版本）** ：在使用 SQL Server 2008 或 2008 R2 时，JDBC 驱动程序支持 SELECT、DELETE、INSERT 和 UPDATE 语句，前提是这些语句不包含子查询和/或联接。

在使用 SQL Server 2008 或 2008 R2 时，SQLServerParameterMetaData 类也不支持 MERGE 查询。 对于 SQL Server 2012 和较高版本，支持带有复杂查询的参数元数据。

不支持检索已加密列的参数元数据。 **对于 Microsoft JDBC Driver 4.1 或 4.2 for SQL Server**：JDBC 驱动程序支持 SELECT、DELETE、INSERT 和 UPDATE 语句，前提是这些语句不包含子查询和/或联接。 SQLServerParameterMetaData 类也不支持 MERGE 查询。
