---
title: 执行批处理操作 |Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1a576d95-7da6-4b7b-8b32-59e5b4d354c4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4923354c5f6dc013d9fee0284279bb5b6b887556
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801823"
---
# <a name="performing-batch-operations"></a>执行批处理操作
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  为了提高对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库进行多项更新时的性能，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供了将多项更新作为一个工作单元提交的功能，也称作“批”。  
  
 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)、[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 和 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 类都可用于提交批量更新。 [addBatch](../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md) 方法可用于添加命令。 [clearBatch](../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md) 方法可用于清除命令列表。 [executeBatch](../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md) 方法可用于提交要处理的所有命令。 只有返回简单更新计数的数据定义语言 (Data Definition Language, DDL) 和数据操作语言 (Data Manipulation Language, DML) 语句可作为批处理的一部分运行。  
  
 executeBatch 方法返回一个由 int 值组成的数组，这些值对应于每个命令的更新计数  。 如果一个命令失败，将引发 BatchUpdateException，并且应使用 BatchUpdateException 类的 getUpdateCounts 方法来检索更新计数数组。 如果一条命令失败，则驱动程序会继续处理剩余的命令。 但是，如果一条命令有语法错误，批处理中的语句就会失败。  
  
> [!NOTE]  
>  如果不是必须使用更新计数，则可以先向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发送一条 SET NOCOUNT ON 语句。 这将减少网络流量并同时提高应用程序的性能。  
  
 例如，在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库中创建下表：  
  
```sql
CREATE TABLE TestTable   
   (Col1 int IDENTITY,   
    Col2 varchar(50),   
    Col3 int);  
```  
  
 在下面的实例中，将向此函数传递 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库的打开连接，并使用 addBatch 方法创建要执行的语句，然后调用 executeBatch 方法向数据库提交批处理。  
  
```java
public static void executeBatchUpdate(Connection con) {  
   try {  
      Statement stmt = con.createStatement();  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('X', 100)");  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('Y', 200)");  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('Z', 300)");  
      int[] updateCounts = stmt.executeBatch();  
      stmt.close();  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [通过 JDBC 驱动程序使用语句](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
