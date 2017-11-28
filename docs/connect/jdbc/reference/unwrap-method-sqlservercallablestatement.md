---
title: "unwrap 方法 (SQLServerCallableStatement) |Microsoft 文档"
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
ms.assetid: cbbf2728-b8c8-4c35-875a-6e967c8285dc
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: df50ce32ceb12f89e83bfb8135609b4234ee8074
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="unwrap-method-sqlservercallablestatement"></a>unwrap 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回一个实现指定的接口，以允许访问的对象[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]的特定方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>Parameters  
 *iface*  
  
 类型的类**T**定义的接口。  
  
## <a name="return-value"></a>返回值  
 实现指定接口的对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 [Unwrap](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)由 java.sql.Wrapper 接口，在引入 JDBC 4.0 规范中定义方法。  
  
 应用程序可能需要访问特定于 JDBC API 扩展[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]。 Unwrap 方法支持解包到此对象扩展的公共类，如果类公开供应商扩展。  
  
 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)实现[ISQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)，从扩展[ISQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。 当调用此方法时，该对象解包到以下类： [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)， [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)，和[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)。  
  
 有关详细信息，请参阅[包装和接口](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
 下面的代码示例演示如何使用 isWrapperFor 和 unwrap 方法来检查驱动程序扩展和调用特定于供应商的方法，如[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)和[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)。  
  
```  
public static void executeStoredProcedure(Connection con) {  
   try {  
    CallableStatement cstmt =   
       con.prepareCall("{call dbo.stored_proc_name(?, ?)}");  
  
    // The recommended way to access the JDBC   
    // Driver-specific methods is to use the JDBC 4.0 Wrapper   
    // functionality.   
    // The following code statements demonstrates how to use the   
    // isWrapperFor and unwrap methods  
    // to access the driver-specific response buffering methods.  
  
    if (cstmt.isWrapperFor(  
      com.microsoft.sqlserver.jdbc.SQLServerCallableStatement.class)) {  
     // The CallableStatement object can unwrap to   
     // SQLServerCallableStatement.  
     SQLServerCallableStatement SQLcstmt =   
     cstmt.unwrap(  
        com.microsoft.sqlserver.jdbc.SQLServerCallableStatement.class);  
     SQLcstmt.setResponseBuffering("adaptive");  
     System.out.println("Response buffering mode has been set to " +  
         SQLcstmt.getResponseBuffering());  
     }  
  
    if (cstmt.isWrapperFor(  
      com.microsoft.sqlserver.jdbc.SQLServerPreparedStatement.class)) {  
      // The CallableStatement object can unwrap to   
      // SQLServerPreparedStatement.                    
      SQLServerPreparedStatement SQLpstmt =   
       cstmt.unwrap(  
       com.microsoft.sqlserver.jdbc.SQLServerPreparedStatement.class);  
      SQLpstmt.setResponseBuffering("adaptive");  
      System.out.println("Response buffering mode has been set to " +  
          SQLpstmt.getResponseBuffering());  
    }  
    if (cstmt.isWrapperFor(  
      com.microsoft.sqlserver.jdbc.SQLServerStatement.class)) {  
  
      // The CallableStatement object can unwrap to SQLServerStatement.   
      SQLServerStatement SQLstmt =   
        cstmt.unwrap(  
        com.microsoft.sqlserver.jdbc.SQLServerStatement.class);  
      SQLstmt.setResponseBuffering("adaptive");  
      System.out.println("Response buffering mode has been set to " +  
      SQLstmt.getResponseBuffering());  
    }  
  }  
  catch (Exception e) {  
     e.printStackTrace();  
  }  
}   
```  
  
## <a name="see-also"></a>另请参阅  
 [isWrapperFor 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
