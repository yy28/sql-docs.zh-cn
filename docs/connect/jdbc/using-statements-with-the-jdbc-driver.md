---
title: 通过 JDBC 驱动程序使用语句 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7f8f3e8f-841e-4449-9154-b5366870121f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9ddd61d15e3c363766c7e49b8e9045b60a7be164
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "69025787"
---
# <a name="using-statements-with-the-jdbc-driver"></a>通过 JDBC 驱动程序使用语句

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

可以通过多种方式使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 来处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的数据。 JDBC 驱动程序可用于运行针对数据库的 SQL 语句，也可用于通过使用输入和输出参数来调用数据库中的存储过程。 JDBC 驱动程序还支持使用 SQL 转义序列、更新计数、自动生成的键，并支持在批处理操作内执行更新。  
  
JDBC 驱动程序提供了三个从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库检索数据的类：  
  
1. [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) - 用于运行不带参数的 SQL 语句。  
  
2. [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) -（继承自 SQLServerStatement），用于运行编译的可能包含 IN 参数的 SQL 语句。  
  
3. [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) -（继承自 SQLServerPreparedStatement），用于运行可能包含 IN 参数、OUT 参数或两者都包含的存储过程。  
  
 本部分中的主题讨论如何使用这三个语句类中的各个类来处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的数据。  
  
## <a name="in-this-section"></a>在本节中  

| 主题                                                                                                    | 说明                                                                                                                                            |
| -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [使用 SQL 语句](../../connect/jdbc/using-statements-with-sql.md)                             | 说明如何通过 JDBC 驱动程序使用 SQL 语句来处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的数据。    |
| [结合使用语句和存储过程](../../connect/jdbc/using-statements-with-stored-procedures.md) | 说明如何通过 JDBC 驱动程序使用存储过程来处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的数据。 |
| [使用多个结果集](../../connect/jdbc/using-multiple-result-sets.md)                           | 说明如何使用 JDBC 驱动程序从多个结果集检索数据。                                                                       |
| [使用 SQL 转义序列](../../connect/jdbc/using-sql-escape-sequences.md)                           | 说明如何使用 SQL 转义序列，例如日期和时间原义字符和函数。                                                               |
| [使用自动生成键](../../connect/jdbc/using-auto-generated-keys.md)                             | 说明如何使用自动生成的键。                                                                                                     |
| [执行批量操作](../../connect/jdbc/performing-batch-operations.md)                         | 说明如何使用 JDBC 驱动程序执行批处理操作。                                                                                      |
| [处理复杂语句](../../connect/jdbc/handling-complex-statements.md)                         | 说明如何使用 JDBC 驱动程序运行复杂语句，这些语句执行多种任务并且可能返回不同类型的数据。               |
  
## <a name="see-also"></a>另请参阅

[JDBC 驱动程序概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
