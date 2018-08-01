---
title: 通过 JDBC 驱动程序使用语句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7f8f3e8f-841e-4449-9154-b5366870121f
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c7da2ce5f69df8f28b281a935ea938b2648fa555
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37968930"
---
# <a name="using-statements-with-the-jdbc-driver"></a>通过 JDBC 驱动程序使用语句
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  可以通过多种方式使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 来处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据库中的数据。 JDBC 驱动程序可用于运行针对数据库的 SQL 语句，也可用于通过使用输入和输出参数来调用数据库中的存储过程。 JDBC 驱动程序还支持使用 SQL 转义序列、更新计数、自动生成的键，并支持在批处理操作内执行更新。  
  
 JDBC 驱动程序提供了三个从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据库检索数据的类：  
  
1.  [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) - 用于运行不带参数的 SQL 语句。  
  
2.  [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) -（继承自 SQLServerStatement），用于运行编译的可能包含 IN 参数的 SQL 语句。  
  
3.  [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) -（继承自 SQLServerPreparedStatement），用于运行可能包含 IN 参数、OUT 参数或两者都包含的存储过程。  
  
 本部分中的主题讨论如何使用这三个语句类中的各个类来处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据库中的数据。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|描述|  
|-----------|-----------------|  
|[使用 SQL 语句](../../connect/jdbc/using-statements-with-sql.md)|说明如何通过 JDBC 驱动程序使用 SQL 语句来处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据库中的数据。|  
|[在存储过程中使用语句](../../connect/jdbc/using-statements-with-stored-procedures.md)|说明如何通过 JDBC 驱动程序使用存储过程来处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据库中的数据。|  
|[使用多个结果集](../../connect/jdbc/using-multiple-result-sets.md)|说明如何使用 JDBC 驱动程序从多个结果集检索数据。|  
|[使用 SQL 转义序列](../../connect/jdbc/using-sql-escape-sequences.md)|说明如何使用 SQL 转义序列，例如日期和时间原义字符和函数。|  
|[使用自动生成的键](../../connect/jdbc/using-auto-generated-keys.md)|说明如何使用自动生成的键。|  
|[执行批处理操作](../../connect/jdbc/performing-batch-operations.md)|说明如何使用 JDBC 驱动程序执行批处理操作。|  
|[处理复杂语句](../../connect/jdbc/handling-complex-statements.md)|说明如何使用 JDBC 驱动程序运行复杂语句，这些语句执行多种任务并且可能返回不同类型的数据。|  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
