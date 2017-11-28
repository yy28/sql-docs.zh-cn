---
title: "执行批处理操作 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1a576d95-7da6-4b7b-8b32-59e5b4d354c4
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 44acde56f2ddc25c66b7e896089499c5597ae779
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="performing-batch-operations"></a>执行批处理操作
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  若要提高性能，当多个更新到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]发生的数据库，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供作为一个单元的工作，也称为一个批次提交多个更新的能力。  
  
 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)， [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)，和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类都可以用来提交批处理更新。 [AddBatch](../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md)方法用于将命令添加。 [ClearBatch](../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md)方法用于清除的命令的列表。 [ExecuteBatch](../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md)方法用于提交以进行处理的所有命令。 只有返回简单更新计数的数据定义语言 (Data Definition Language, DDL) 和数据操作语言 (Data Manipulation Language, DML) 语句可作为批处理的一部分运行。  
  
 ExecuteBatch 方法返回的数组**int**对应于每个命令将更新计数的值。 如果其中一个命令失败，引发 BatchUpdateException，并且应该使用 BatchUpdateException 类的 getUpdateCounts 方法来检索更新计数数组。 如果一条命令失败，则驱动程序会继续处理剩余的命令。 但是，如果一条命令有语法错误，批处理中的语句就会失败。  
  
> [!NOTE]  
>  如果不需要使用更新计数，你可以首先发出 SET NOCOUNT ON 语句与[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 这将减少网络流量并同时提高应用程序的性能。  
  
 例如，创建下的表中[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库：  
  
```  
CREATE TABLE TestTable   
   (Col1 int IDENTITY,   
    Col2 varchar(50),   
    Col3 int);  
```  
  
 在下面的示例中，与的开放连接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库中传递给函数、 addBatch 方法用于创建要执行的语句和 executeBatch 方法被调用以提交到数据库批处理。  
  
```  
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
  
  
