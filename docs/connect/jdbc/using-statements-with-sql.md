---
title: Using 语句与 SQL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fe28f48a-e1bc-48ff-a5e7-c24cd6e5ecc7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 082671d3acf2873bb822e6b836599c00f42d6323
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916163"
---
# <a name="using-statements-with-sql"></a>使用 SQL 语句

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和内联 SQL 语句处理 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 数据库中的数据时，有多个不同的类可供使用。 使用哪个类取决于要运行的 SQL 语句的类型。  
  
如果 SQL 语句不包含 IN 参数，则使用 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 类；但如果包含 IN 参数，则使用 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 类。  
  
> [!NOTE]  
> 如果需要使用同时包含 IN 和 OUT 参数的 SQL 语句，则必须将这些语句作为存储过程来实现，并使用 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 类对其进行调用。 有关使用存储过程的详细信息, 请参阅[使用存储过程的语句](../../connect/jdbc/using-statements-with-stored-procedures.md)。  
  
下列部分说明了使用 SQL 语句来处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中数据的不同方案。  

## <a name="in-this-section"></a>本节内容  

| 主题                                                                                                                        | 描述                                                       |
| ---------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| [使用不带参数的 SQL 语句](../../connect/jdbc/using-an-sql-statement-with-no-parameters.md)                 | 说明如何使用不包含参数的 SQL 语句。   |
| [使用带参数的 SQL 语句](../../connect/jdbc/using-an-sql-statement-with-parameters.md)                       | 说明如何使用包含参数的 SQL 语句。      |
| [使用 SQL 语句修改数据库对象](../../connect/jdbc/using-an-sql-statement-to-modify-database-objects.md) | 说明如何使用 SQL 语句修改数据库对象。   |
| [使用 SQL 语句修改数据](../../connect/jdbc/using-an-sql-statement-to-modify-data.md)                         | 说明如何使用 SQL 语句修改数据库中的数据。 |
  
## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序使用语句](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
