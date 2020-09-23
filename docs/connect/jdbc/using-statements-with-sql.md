---
title: 使用 SQL 语句
description: 大致了解如何将不同类型的 SQL 语句与 Microsoft JDBC Driver for SQL Server 一起使用。
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fe28f48a-e1bc-48ff-a5e7-c24cd6e5ecc7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 49ab0f6367353847bdf3a9e0a7aff13975b4d711
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435287"
---
# <a name="using-statements-with-sql"></a>使用 SQL 语句

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和内联 SQL 语句处理 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 数据库中的数据时，有多个不同的类可供使用。 使用哪个类取决于要运行的 SQL 语句的类型。  
  
如果 SQL 语句不包含 IN 参数，则使用 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 类；但如果包含 IN 参数，则使用 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 类。  
  
> [!NOTE]  
> 如果需要使用同时包含 IN 和 OUT 参数的 SQL 语句，则必须将这些语句作为存储过程来实现，并使用 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 类对其进行调用。 有关使用存储过程的详细信息，请参阅[结合使用语句和存储过程](../../connect/jdbc/using-statements-with-stored-procedures.md)。  
  
下列部分说明了使用 SQL 语句来处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中数据的不同方案。  

## <a name="in-this-section"></a>本节内容  

| 主题                                                                                                                        | 说明                                                       |
| ---------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| [使用不含参数的 SQL 语句](../../connect/jdbc/using-an-sql-statement-with-no-parameters.md)                 | 说明如何使用不包含参数的 SQL 语句。   |
| [使用含参数的 SQL 语句](../../connect/jdbc/using-an-sql-statement-with-parameters.md)                       | 说明如何使用包含参数的 SQL 语句。      |
| [使用 SQL 语句修改数据库对象](../../connect/jdbc/using-an-sql-statement-to-modify-database-objects.md) | 说明如何使用 SQL 语句修改数据库对象。   |
| [使用 SQL 语句修改数据](../../connect/jdbc/using-an-sql-statement-to-modify-data.md)                         | 说明如何使用 SQL 语句修改数据库中的数据。 |
  
## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序使用语句](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
