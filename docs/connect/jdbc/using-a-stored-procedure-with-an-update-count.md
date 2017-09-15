---
title: "使用更新计数的存储的过程 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 64cf4877-5995-4bfc-8865-b7618a5c8d01
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fb038eeb3b3b0f14ef0ace1076244bd64949ed81
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-a-stored-procedure-with-an-update-count"></a>使用带有更新计数的存储过程
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  在中修改数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]通过使用存储的过程中，数据库[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类。 通过使用 SQLServerCallableStatement 类，你可以调用存储的过程修改数据库中包含的数据，并返回受影响的行数的计数也称为更新计数。  
  
 使用 SQLServerCallableStatement 类设置了对存储过程的调用后，然后可以通过使用调用存储的过程[执行](../../connect/jdbc/reference/execute-method-sqlserverstatement.md)或[executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)方法。 ExecuteUpdate 方法将返回**int**包含受影响的存储的过程，但执行方法的行号的值却没有。 如果你使用 execute 方法，并想要获取的影响的行数的计数，则可以调用[getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)后运行存储的过程的方法。  
  
> [!NOTE]  
>  如果要让 JDBC 驱动程序返回所有更新计数，包括任何可能已不再使用的触发器所返回的更新计数，请将 lastUpdateCount 连接字符串属性设置为“false”。 有关 lastUpdateCount 属性的详细信息，请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
 例如，创建以下表和存储的过程，并还插入中的示例数据[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库：  
  
```  
CREATE TABLE TestTable   
   (Col1 int IDENTITY,   
    Col2 varchar(50),   
    Col3 int);  
  
CREATE PROCEDURE UpdateTestTable  
   @Col2 varchar(50),  
   @Col3 int  
AS  
BEGIN  
   UPDATE TestTable  
   SET Col2 = @Col2, Col3 = @Col3  
END;  
INSERT INTO dbo.TestTable (Col2, Col3) VALUES ('b', 10);  
```  
  
 在下面的示例中，与的开放连接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库中传递给函数，execute 方法用于调用 UpdateTestTable 存储过程中，并且然后 getUpdateCount 方法用于返回的行的计数受影响的存储过程。  
  
 [!code[JDBC#UsingSprocWithUpdateCount1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_0_1.java)]  
  
## <a name="see-also"></a>另请参阅  
 [使用存储过程的语句](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  
