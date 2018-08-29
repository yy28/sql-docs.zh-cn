---
title: 配置如何将 java.sql.Time 值发送到服务器 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 07eb00dd-621a-46f9-a5a5-8cab4d6058b5
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fcb15ace351d53ed072738ea9e8978eb681294b0
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42787139"
---
# <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>配置如何将 java.sql.Time 值发送到服务器
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  如果使用 java.sql.Time 对象或 java.sql.Types.TIME JDBC 类型设置参数，可以配置如何将 java.sql.Time 值发送到服务器，即作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] time 类型还是 datetime 类型发送。  
  
 使用以下方法之一时适用此方案：  
  
-   [SQLServerCallableStatement.registerOutParameter(int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int.md)  
  
-   [SQLServerCallableStatement.registerOutParameter(int, int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int-int.md)  
  
-   [SQLServerCallableStatement.setTime](../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setTime](../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)  
  
-   [SQLServerCallableStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)  
  
 可以通过使用 sendTimeAsDatetime 连接属性配置如何发送 java.sql.Time 值。 有关详细信息，请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
 可以通过编程使用 [SQLServerDataSource.setSendTimeAsDatetime](../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) 修改 sendTimeAsDatetime 连接属性的值。  
  
 新版[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]早于[!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]不支持**时间**数据类型，因此通常使用 java.sql.Time 的应用程序存储 java.sql.Time 值作为**datetime**或**smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型。  
  
 如果你想要使用**datetime**并**smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型在处理 java.sql.Time 值时，应设置**sendTimeAsDatetime**连接属性设置为 **，则返回 true**。 如果你想要使用**时间**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型时使用 java.sql.Time 值时，应设置**sendTimeAsDatetime**连接属性设置为**false**.  
  
 请注意，在将 java.sql.Time 值发送给其数据类型还存储日期的参数时，默认日期会有所不同，具体取决于 java.sql.Time 值是作为 datetime (1/1/1970) 还是 time (1/1/1900) 值发送。 有关将数据发送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时的数据转换的详细信息，请参阅[使用日期和时间数据](http://go.microsoft.com/fwlink/?LinkID=145211)。  
  
 在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]JDBC Driver 3.0 **sendTimeAsDatetime**是默认情况下，则返回 true。 在将来的发行版中，默认情况下可以将 sendTimeAsDatetime 连接属性设置为 false。  
  
 为了确保无论 sendTimeAsDatetime 连接属性的默认值为什么，应用程序都能正常工作，可以：  
  
-   在使用 time[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型时使用 java.sql.Time。  
  
-   处理时使用 java.sql.Timestamp **datetime**， **smalldatetime**，并**datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型。  
  
因为加密的列不支持从时间转换为 datetime，SendTimeAsDatetime 必须为假加密列。 从 Microsoft JDBC Driver 6.0 for SQL Server，SQLServerConnection 类具有以下两种方法来设置/获取 sendTimeAsDatetime 属性的值。

```java
  public boolean getSendTimeAsDatetime()
  public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
```
  
## <a name="see-also"></a>另请参阅  
 [了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
