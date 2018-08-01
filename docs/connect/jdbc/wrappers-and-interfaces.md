---
title: 包装和接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 27fc9b72-9f21-4728-abcb-5c015f28a6ab
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9a7316e5daa6fa27209a31a07ddf0ace84c191b0
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37994805"
---
# <a name="wrappers-and-interfaces"></a>包装和接口
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支持允许你创建类的代理的接口，并且支持允许你通过代理接口访问（特定于 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]的）JDBC API 扩展的包装器。  
  
## <a name="wrappers"></a>包装  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支持 java.sql.Wrapper 接口。 该接口提供一种机制，通过代理接口访问特定于 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 的 JDBC API 扩展。  
  
 Java.sql.Wrapper 接口定义两个方法： **isWrapperFor**并**unwrap**。 isWrapperFor 方法检查指定的输入对象是否实现此接口。 unwrap 方法返回一个实现此接口的对象，从而允许访问特定于 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 的方法。  
  
 **isWrapperFor**并**unwrap**方法公开，如下所示：  
  
-   [isWrapperFor 方法 (SQLServerCallableStatement)](../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)  
  
-   [unwrap 方法 (SQLServerCallableStatement)](../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)  
  
-   [isWrapperFor 方法 (SQLServerConnectionPoolDataSource)](../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)  
  
-   [unwrap 方法 (SQLServerConnectionPoolDataSource)](../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)  
  
-   [isWrapperFor 方法 (SQLServerDataSource)](../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)  
  
-   [unwrap 方法&#40;SQLServerDataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)  
  
-   [isWrapperFor 方法 (SQLServerPreparedStatement)](../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)  
  
-   [unwrap 方法 (SQLServerPreparedStatement)](../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)  
  
-   [isWrapperFor 方法 (SQLServerStatement)](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)  
  
-   [unwrap 方法&#40;SQLServerStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)  
  
-   [isWrapperFor 方法 (SQLServerXADataSource)](../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md)  
  
-   [unwrap 方法&#40;SQLServerXADataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)  
  
## <a name="interfaces"></a>界面  
 从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] JDBC Driver 3.0 开始，接口可用于应用程序服务器，以便从关联的类访问驱动程序特定的方法。 应用程序服务器通过创建代理对类进行包装，并且从接口公开 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 特定的函数。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支持具有 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 特定的方法和常量的接口，因此应用程序服务器可以创建类的代理。  
  
 这些接口派生自标准 Java 接口，这样，取消对接口的包装后访问驱动程序特定的功能或一般 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 功能时，就可以使用相同的对象。  
  
 新增了以下接口：  
  
-   [ISQLServerCallableStatement](../../connect/jdbc/reference/isqlservercallablestatement-interface.md)  
  
-   [ISQLServerConnection](../../connect/jdbc/reference/isqlserverconnection-interface.md)  
  
-   [ISQLServerDataSource](../../connect/jdbc/reference/isqlserverdatasource-interface.md)  
  
-   [ISQLServerPreparedStatement](../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
-   [ISQLServerResultSet](../../connect/jdbc/reference/isqlserverresultset-interface.md)  
  
-   [ISQLServerStatement](../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 此示例说明如何从 DataSource 对象访问 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 特定的函数。 此 DataSource 类可能已由应用程序服务器包装。 若要访问 JDBC 驱动程序特定的函数或常量，可以取消数据源对 ISQLServerDataSource 接口的数据源的包装，并使用在此接口中声明的函数。  
  
### <a name="code"></a>代码  
  
```  
import javax.sql.*;  
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.*;  
  
public class UnWrapTest {  
   public static void main(String[] args) {  
      // This is a test.  This DataSource object could be something from an appserver   
      // which has wrapped the real SQLServerDataSource with its own wrapper  
      SQLServerDataSource ds = new SQLServerDataSource();  
      checkSendStringParametersAsUnicode(ds);  
   }  
  
   // Unwrap to the ISQLServerDataSource interface to access the getSendStringParametersAsUnicode function  
   static void checkSendStringParametersAsUnicode(DataSource ds) {  
      try {  
         final ISQLServerDataSource sqlServerDataSource = ds.unwrap(ISQLServerDataSource.class);  
         boolean sendStringParametersAsUnicode = sqlServerDataSource.getSendStringParametersAsUnicode();  
  
         System.out.println("Send string as parameter value is:-" + sendStringParametersAsUnicode);  
  
      } catch (SQLException sqlE) {  
         System.out.println("Exception:-" + sqlE);  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
