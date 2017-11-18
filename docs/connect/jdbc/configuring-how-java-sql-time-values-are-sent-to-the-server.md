---
title: "配置如何将 java.sql.Time 值发送到服务器 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 07eb00dd-621a-46f9-a5a5-8cab4d6058b5
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3fc45c7fc45bb37ea9373c452a2086557ecf62fc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>配置如何将 java.sql.Time 值发送到服务器
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  如果你使用 java.sql.Time 对象或 java.sql.Types.TIME JDBC 类型设置的参数，则可以配置如何将 java.sql.Time 值发送到服务器;可作为[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**时间**类型或**datetime**类型。  
  
 使用以下方法之一时适用此方案：  
  
-   [SQLServerCallableStatement.registerOutParameter （int，int）](../../connect/jdbc/reference/registeroutparameter-method-int-int.md)  
  
-   [SQLServerCallableStatement.registerOutParameter （int、 int、 int）](../../connect/jdbc/reference/registeroutparameter-method-int-int-int.md)  
  
-   [SQLServerCallableStatement.setTime](../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setTime](../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)  
  
-   [SQLServerCallableStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)  
  
 你可以配置如何将 java.sql.Time 值发送使用**sendTimeAsDatetime**连接属性。 有关详细信息，请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
 你可以以编程方式修改的值**sendTimeAsDatetime**连接属性[SQLServerDataSource.setSendTimeAsDatetime](../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。  
  
 版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]早于[!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]不支持**时间**数据类型，因此，应用程序通常使用 java.sql.Time 存储 java.sql.Time 值作为**datetime**或**smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型。  
  
 如果你想要使用**datetime**和**smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型使用 java.sql.Time 值时，应设置**sendTimeAsDatetime**连接属性设置为**true**。 如果你想要使用**时间**[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型时使用 java.sql.Time 值时，应设置**sendTimeAsDatetime**连接属性设置为**false**.  
  
 请注意，当其数据类型将 java.sql.Time 值发送到参数还可以将存储的日期，默认日期是不同，具体取决于是否将 java.sql.Time 值发送作为**datetime** （1970 年 1 月 1） 或**时间**(1/1/1900) 值。 有关数据转换时将数据发送到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，请参阅[使用日期和时间数据](http://go.microsoft.com/fwlink/?LinkID=145211)。  
  
 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]JDBC Driver 3.0 **sendTimeAsDatetime**是默认情况下如此。 在未来版本中， **sendTimeAsDatetime**连接属性可能默认情况下设置为 false。  
  
 若要确保你的应用程序继续按预期方式而不考虑默认值的工作**sendTimeAsDatetime**连接属性，你可以：  
  
-   处理时使用 java.sql.Time**时间**[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型。  
  
-   处理时使用 java.sql.Timestamp **datetime**， **smalldatetime**，和**datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型。  
  
请注意该 sendTimeAsDatetime 必须为假加密列，因为加密的列不支持从时间转换为日期时间。 从 SQL Server 的 Microsoft JDBC Driver 6.0，SQLServerConnection 类具有以下两个方法来设置/获取 sendTimeAsDatetime 属性的值。

```
  public boolean getSendTimeAsDatetime()
  public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
```
  
## <a name="see-also"></a>另请参阅  
 [了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  

