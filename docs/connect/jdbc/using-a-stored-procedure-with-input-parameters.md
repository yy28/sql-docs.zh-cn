---
title: 使用含输入参数的存储过程 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8f491b70-7d1b-42bd-964f-9a8b86af5eaa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c84e4081b9369d504d173387c6944b06d927c9c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "69026897"
---
# <a name="using-a-stored-procedure-with-input-parameters"></a>使用含输入参数的存储过程

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

可以调用包含一个或多个 IN 参数的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程，这些参数可用于向存储过程传递数据。 可以使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供的 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 类，调用此类存储过程并处理其返回的数据。

使用 JDBC 驱动程序调用带 IN 参数的存储过程时，必须结合 `call`SQLServerConnection[ 类的 ](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)prepareCall[ 方法使用 ](../../connect/jdbc/reference/sqlserverconnection-class.md) SQL 转义序列。 带有 IN 参数的 `call` 转义序列的语法如下所示：

`{call procedure-name[([parameter][,[parameter]]...)]}`

> [!NOTE]  
> 若要详细了解 SQL 转义序列，请参阅[使用 SQL 转义序列](../../connect/jdbc/using-sql-escape-sequences.md)。

构造 `call` 转义序列时，请使用 ?（问号）字符 来指定 IN 参数。 此字符充当要传递给该存储过程的参数值的占位符。 可以使用 SQLServerPreparedStatement 类的 setter 方法之一为参数指定值。 可使用的 setter 方法由 IN 参数的数据类型决定。

向 setter 方法传递值时，不仅需要指定要在参数中使用的实际值，还必须指定参数在存储过程中的序数位置。 例如，如果存储过程包含单个 IN 参数，则其序数值为 1。 如果存储过程包含两个参数，则第一个序数值为 1，第二个序数值为 2。

作为如何调用包含 IN 参数的存储过程的实例，使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库中的 uspGetEmployeeManagers 存储过程。 此存储过程接受名为 EmployeeID 的单个输入参数（它是一个整数值），然后基于指定的 EmployeeID 返回雇员及其经理的递归列表。 下面是调用此存储过程的 Java 代码：

```java
public static void executeSprocInParams(Connection con) throws SQLException {  
    try(PreparedStatement pstmt = con.prepareStatement("{call dbo.uspGetEmployeeManagers(?)}"); ) {  

        pstmt.setInt(1, 50);  
        ResultSet rs = pstmt.executeQuery();  

        while (rs.next()) {  
            System.out.println("EMPLOYEE:");  
            System.out.println(rs.getString("LastName") + ", " + rs.getString("FirstName"));  
            System.out.println("MANAGER:");  
            System.out.println(rs.getString("ManagerLastName") + ", " + rs.getString("ManagerFirstName"));  
            System.out.println();  
        }  
    }
}
```

## <a name="see-also"></a>另请参阅

[结合使用语句和存储过程](../../connect/jdbc/using-statements-with-stored-procedures.md)
