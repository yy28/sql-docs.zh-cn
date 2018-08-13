---
title: 使用带有更新计数的存储过程 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 64cf4877-5995-4bfc-8865-b7618a5c8d01
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cebd655a20c49525585cb414cfd7409745391bdc
ms.sourcegitcommit: 2f9cafc1d7a3773a121bdb78a095018c8b7c149f
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/08/2018
ms.locfileid: "39662119"
---
# <a name="using-a-stored-procedure-with-an-update-count"></a>使用带有更新计数的存储过程

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

为了使用存储过程修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据库中的数据，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供了 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 类。 通过使用 SQLServerCallableStatement 类，可以调用修改数据库中数据的存储过程，然后返回受影响的行数计数（也称为更新计数）。

使用 SQLServerCallableStatement 类构建对存储过程的调用之后，可以使用 [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 或 [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) 方法中的任意一个来调用此存储过程。 executeUpdate 方法将返回一个 int 值，该值包含受此存储过程影响的行数，但 execute 方法不返回此值。 如果使用 execute 方法，并且希望获得受影响的行数计数，则可以在运行存储过程后调用 [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) 方法。

> [!NOTE]  
> 如果要让 JDBC 驱动程序返回所有更新计数，包括任何可能已不再使用的触发器所返回的更新计数，请将 lastUpdateCount 连接字符串属性设置为“false”。 有关 lastUpdateCount 属性的详细信息，请参阅[连接属性设置](../../connect/jdbc/setting-the-connection-properties.md)。

作为示例，在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库中创建以下表和存储过程，以及插入示例数据：

```sql
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

在下面的示例中，将向此函数传递 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库的打开连接，并使用 execute 方法调用 UpdateTestTable 存储过程，然后使用 getUpdateCount 方法返回受存储过程影响的行计数。

[!code[JDBC#UsingSprocWithUpdateCount1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_0_1.java)]

## <a name="see-also"></a>另请参阅

[在存储过程中使用语句](../../connect/jdbc/using-statements-with-stored-procedures.md)
