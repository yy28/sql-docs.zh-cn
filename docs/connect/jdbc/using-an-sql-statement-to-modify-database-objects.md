---
title: "使用 SQL 语句来修改数据库对象 |Microsoft 文档"
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
ms.assetid: f49ea499-df3c-4e85-9fc7-450fb99622a6
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c5bc8d1f8ce376595a2daf1cc8fddd240a2b4ba8
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="using-an-sql-statement-to-modify-database-objects"></a>使用 SQL 语句修改数据库对象
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  若要修改[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]通过使用 SQL 语句的数据库对象，则可以使用[executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)类。 ExecuteUpdate 方法将传递给以进行处理，数据库的 SQL 语句，然后返回值为 0，因为不影响了任何行。  
  
 若要执行此操作，你必须首先创建 SQLServerStatement 对象使用[createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)类。  
  
> [!NOTE]  
>  修改数据库中对象的 SQL 语句称为“数据定义语言 (Data Definition Language, DDL)”语句。 这些语句包括 CREATE TABLE、DROP TABLE、CREATE INDEX 和 DROP INDEX 之类的语句。 有关支持的 DDL 语句的类型的详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，请参阅[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]联机丛书。  
  
 在下面的示例中，与的开放连接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库中传递给函数、 构造 SQL 语句，它将在数据库中，创建简单 TestTable 然后运行该语句并显示返回的值。  
  
 [!code[JDBC#UsingSQLToModifyDBObjects1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_0_1.java)]  
  
## <a name="see-also"></a>另请参阅  
 [使用 SQL 语句](../../connect/jdbc/using-statements-with-sql.md)  
  
  
