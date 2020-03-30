---
title: 使用不含参数的存储过程 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e9470a6d-a758-4c56-96ec-7b37139e36a7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 01f59f44d42af1d0880df48b043080525d9821ee
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027023"
---
# <a name="using-a-stored-procedure-with-no-parameters"></a>使用不含参数的存储过程

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

在可以调用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程中，最简单的类型是不包含任何参数并且返回单个结果集的存储过程。 可以使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供的 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 类来调用此类存储过程并处理其返回的数据。

使用 JDBC 驱动程序调用不带参数的存储过程时，必须使用 `call` SQL 转义序列。 不带参数的 `call` 转义序列的语法如下所示：

`{call procedure-name}`

> [!NOTE]  
> 若要详细了解 SQL 转义序列，请参阅[使用 SQL 转义序列](../../connect/jdbc/using-sql-escape-sequences.md)。

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

[结合使用语句和存储过程](../../connect/jdbc/using-statements-with-stored-procedures.md)
