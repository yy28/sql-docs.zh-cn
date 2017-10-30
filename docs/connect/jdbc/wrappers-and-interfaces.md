---
title: "包装和接口 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27fc9b72-9f21-4728-abcb-5c015f28a6ab
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7de6c4bb3e3bb28fefb5eba0fa52a5de8684fa6d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="wrappers-and-interfaces"></a>包装和接口
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支持接口，允许你创建的类，代理和包装，让你访问 JDBC API 所特有的扩展[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]通过代理的接口。  
  
## <a name="wrappers"></a>包装  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支持 java.sql.Wrapper 接口。 此接口提供某种机制来访问扩展到的 JDBC API 的特定于[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]通过代理的接口。  
  
 Java.sql.Wrapper 接口定义两种方法： **isWrapperFor**和**unwrap**。 **IsWrapperFor**方法检查该指定的输入的对象是否实现此接口。 **Unwrap**方法返回实现此接口可允许访问的对象[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]特定方法。  
  
 **isWrapperFor**和**unwrap**公开的方法，如下所示：  
  
-   [isWrapperFor 方法 &#40;SQLServerCallableStatement &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)  
  
-   [unwrap 方法 &#40;SQLServerCallableStatement &#41;](../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)  
  
-   [isWrapperFor 方法 &#40;SQLServerConnectionPoolDataSource &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)  
  
-   [unwrap 方法 &#40;SQLServerConnectionPoolDataSource &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)  
  
-   [isWrapperFor 方法 &#40;SQLServerDataSource &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)  
  
-   [unwrap 方法 &#40;SQLServerDataSource &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)  
  
-   [isWrapperFor 方法 &#40;SQLServerPreparedStatement &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)  
  
-   [unwrap 方法 &#40;SQLServerPreparedStatement &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)  
  
-   [isWrapperFor 方法 &#40;SQLServerStatement &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)  
  
-   [unwrap 方法 &#40;SQLServerStatement &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)  
  
-   [isWrapperFor 方法 &#40;SQLServerXADataSource &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md)  
  
-   [unwrap 方法 &#40;SQLServerXADataSource &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)  
  
## <a name="interfaces"></a>界面  
 从[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]JDBC Driver 3.0，接口是可用于应用程序服务器关联的类从访问驱动程序的特定方法。 应用程序服务器可以通过创建公开的代理包装类[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]-来自接口的特定功能。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支持接口具有[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]特定的方法和常量，因此应用程序服务器可以创建类的代理。  
  
 接口派生自标准 Java 接口，因此你可以使用相同的对象后打开包装才能访问驱动程序的特定功能或泛型[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]功能。  
  
 新增了以下接口：  
  
-   [ISQLServerCallableStatement](../../connect/jdbc/reference/isqlservercallablestatement-interface.md)  
  
-   [ISQLServerConnection](../../connect/jdbc/reference/isqlserverconnection-interface.md)  
  
-   [ISQLServerDataSource](../../connect/jdbc/reference/isqlserverdatasource-interface.md)  
  
-   [ISQLServerPreparedStatement](../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
-   [ISQLServerResultSet](../../connect/jdbc/reference/isqlserverresultset-interface.md)  
  
-   [ISQLServerStatement](../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>Description  
 此示例演示如何访问[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]-从数据源对象的特定函数。 应用程序服务器可能已包装此数据源类。 若要访问的 JDBC 驱动程序特定的函数或常量，可以解除包装到 ISQLServerDataSource 接口的数据源，并使用在此接口中声明的函数。  
  
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
  
  

