---
title: 使用带有返回状态的存储过程 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4b126e95-8458-41d6-af37-fc6662859f19
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 29bb95c06d86ad4d6e45002da1429f6c7d5a5c9e
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38040595"
---
# <a name="using-a-stored-procedure-with-a-return-status"></a>使用带有返回状态的存储过程
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  可以调用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 存储过程是一个返回状态或结果参数的存储过程。 这通常用于指示存储过程执行成功还是失败。 可以使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供的 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 类，调用此类存储过程并处理其返回的数据。  
  
 使用 JDBC 驱动程序调用这种存储过程时，必须结合 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 类的 [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 方法使用 `call` SQL 转义序列。 返回状态参数的 `call` 转义序列的语法如下所示：  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  有关 SQL 转义序列的详细信息，请参阅[使用 SQL 转义序列](../../connect/jdbc/using-sql-escape-sequences.md)。  
  
 构造 `call` 转义序列时，请使用 ?（问号）字符 来指定 IN 参数。 此字符充当要从该存储过程返回的参数值的占位符。 要为返回状态参数指定值，必须在执行存储过程前使用 SQLServerCallableStatement 类的 [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 方法指定参数的数据类型。  
  
> [!NOTE]  
>  当 JDBC 驱动程序与 SQL Server 数据库一起使用时，registerOutParameter 方法中为返回状态参数指定的值将始终为整数，可通过使用 java.sql.Types.INTEGER 数据类型进行指定。  
  
 此外，向 registerOutParameter 方法传递返回状态参数值时，不仅需要指定要使用的参数的数据类型，还必须指定参数在存储过程中的序数位置。 对于返回状态参数，其序数位置始终为 1，这是因为它始终是调用存储过程时的第一个参数。 尽管 SQLServerCallableStatement 类支持使用参数的名称来指示特定参数，但只能对返回状态参数使用参数的序号位置编号。  
  
 作为示例，在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库中创建以下存储过程：  
  
```  
CREATE PROCEDURE CheckContactCity  
   (@cityName CHAR(50))  
AS  
BEGIN  
   IF ((SELECT COUNT(*)  
   FROM Person.Address  
   WHERE City = @cityName) > 1)  
   RETURN 1  
ELSE  
   RETURN 0  
END  
```  
  
 该存储过程返回状态值 1 或 0，这取决于是否能在表 Person.Address 中找到 cityName 参数指定的城市。  
  
 在下面的实例中，将向此函数传递 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库的打开连接，然后使用 [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 方法调用 CheckContactCity 存储过程：  
  
 [!code[JDBC#UsingSprocWithReturnStatus1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_1_1.java)]  
  
## <a name="see-also"></a>另请参阅  
 [在存储过程中使用语句](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  
