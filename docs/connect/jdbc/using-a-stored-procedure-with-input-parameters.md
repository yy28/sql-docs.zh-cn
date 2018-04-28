---
title: 使用输入参数的存储的过程 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8f491b70-7d1b-42bd-964f-9a8b86af5eaa
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 64bf5a293cbe0f9fd9287a03084d66044a54337a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="using-a-stored-procedure-with-input-parameters"></a>使用带有输入参数的存储过程
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  A[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]可以调用的存储的过程是指包含一个或多在参数中，这是可以用于将数据传递到存储过程的参数。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)类，可用来调用这种类型的存储过程，并处理它将返回的数据。  
  
 当你使用 JDBC 驱动程序来调用存储的过程参数中时，你必须使用`call`一起使用的 SQL 转义序列[prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)类。 语法`call`与参数中的转义序列包含，如下所示：  
  
 `{call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  有关 SQL 转义序列的详细信息，请参阅[使用 SQL 转义序列](../../connect/jdbc/using-sql-escape-sequences.md)。  
  
 构造时`call`转义序列，通过使用指定的 IN 参数？ 来指定 IN 参数。 此字符充当要传递给该存储过程的参数值的占位符。 若要指定参数的值，可以使用 SQLServerPreparedStatement 类的 setter 方法之一。 可使用的 setter 方法由 IN 参数的数据类型决定。  
  
 向 setter 方法传递值时，不仅需要指定要在参数中使用的实际值，还必须指定参数在存储过程中的序数位置。 例如，如果存储过程包含单个 IN 参数，则其序数值为 1。 如果存储过程包含两个参数，则第一个序数值为 1，第二个序数值为 2。  
  
 作为示例，了解如何调用包含 IN 参数的存储的过程，使用中的存储的 uspGetEmployeeManagers 过程[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库。 此存储过程接受名为 EmployeeID 的单个输入参数（它是一个整数值），然后基于指定的 EmployeeID 返回雇员及其经理的递归列表。 下面是调用此存储过程的 Java 代码：  
  
```  
public static void executeSprocInParams(Connection con) {  
   try {  
      PreparedStatement pstmt = con.prepareStatement("{call dbo.uspGetEmployeeManagers(?)}");  
      pstmt.setInt(1, 50);  
      ResultSet rs = pstmt.executeQuery();  
  
      while (rs.next()) {  
         System.out.println("EMPLOYEE:");  
         System.out.println(rs.getString("LastName") + ", " + rs.getString("FirstName"));  
         System.out.println("MANAGER:");  
         System.out.println(rs.getString("ManagerLastName") + ", " + rs.getString("ManagerFirstName"));  
         System.out.println();  
      }  
      rs.close();  
      pstmt.close();  
   }  
  
   catch (Exception e) {  
      e.printStackTrace();  
    }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [在存储过程中使用语句](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  
