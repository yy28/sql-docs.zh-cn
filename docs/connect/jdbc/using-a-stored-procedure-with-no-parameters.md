---
title: 使用不带参数的存储过程 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e9470a6d-a758-4c56-96ec-7b37139e36a7
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d766423b4ee2c1db4b7515c87edfa96b4b84b416
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66790389"
---
# <a name="using-a-stored-procedure-with-no-parameters"></a>使用不带参数的存储过程

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

在可以调用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程中，最简单的类型是不包含任何参数并且返回单个结果集的存储过程。 可以使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供的 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 类来调用此类存储过程并处理其返回的数据。

使用 JDBC 驱动程序调用不带参数的存储过程时，必须使用 `call` SQL 转义序列。 不带参数的 `call` 转义序列的语法如下所示：

`{call procedure-name}`

> [!NOTE]  
> 有关 SQL 转义序列的详细信息，请参阅[使用 SQL 转义序列](../../connect/jdbc/using-sql-escape-sequences.md)。

作为示例，在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库中创建以下存储过程：

```sql
CREATE PROCEDURE GetContactFormalNames
AS  
BEGIN  
   SELECT TOP 10 Title + ' ' + FirstName + ' ' + LastName AS FormalName
   FROM Person.Contact  
END  
```

此存储过程返回单个结果集，其中包含一列数据（由 Person.Contact 表中前 10 个联系人的称呼、名称和姓氏组成）。

在下面的实例中，将向此函数传递 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库的一个打开连接，然后使用 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 方法调用 GetContactFormalNames 存储过程。

```java
public static void executeSprocNoParams(Connection con) throws SQLException {  
    try(Statement stmt = con.createStatement();) {  

        ResultSet rs = stmt.executeQuery("{call dbo.GetContactFormalNames}");  
        while (rs.next()) {  
            System.out.println(rs.getString("FormalName"));  
        }  
    }  
}
```

## <a name="see-also"></a>另请参阅

[在存储过程中使用语句](../../connect/jdbc/using-statements-with-stored-procedures.md)
