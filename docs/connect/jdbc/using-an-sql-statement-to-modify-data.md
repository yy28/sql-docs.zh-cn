---
title: "使用 SQL 语句来修改数据 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4704199b-c0ae-4c77-8a2e-6963715b4ffb
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e913a81f88140c983836d4231ed9c926857f0c14
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-an-sql-statement-to-modify-data"></a>使用 SQL 语句修改数据
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  若要修改中包含的数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库通过使用 SQL 语句，你可以使用[executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)类。 ExecuteUpdate 方法将传递给以进行处理，数据库的 SQL 语句，然后返回一个值，指示受影响的行数。  
  
 若要执行此操作，你必须首先创建 SQLServerStatement 对象使用[createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)类。  
  
 在下面的示例中，与的开放连接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库中传递给函数，SQL 语句将构造该将新数据添加到表中，然后运行该语句并显示返回的值。  
  
 [!code[JDBC#UsingSQLToModifyData1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_1_1.java)]  
  
> [!NOTE]  
>  如果必须使用包含要修改的数据参数的 SQL 语句[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库，则应使用[executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)方法[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)类。  
>   
>  如果试图向其中插入数据的列包含特殊字符（例如空格），则必须提供要插入的值，即使它们是默认值也必须提供。 如果不执行此操作，插入操作就会失败。  
>   
>  如果要让 JDBC 驱动程序返回所有更新计数，包括任何可能已不再使用的触发器所返回的更新计数，请将 lastUpdateCount 连接字符串属性设置为“false”。 有关 lastUpdateCount 属性的详细信息，请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
## <a name="see-also"></a>另请参阅  
 [使用 SQL 语句](../../connect/jdbc/using-statements-with-sql.md)  
  
  
