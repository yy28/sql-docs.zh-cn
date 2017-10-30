---
title: "SQLServerPreparedStatement 成员 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2363902f-d4c6-4cd4-a5fc-86079eb9e418
caps.latest.revision: 38
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 89955e45eacf8c4b9331276706bcbebbe6ab9948
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverpreparedstatement-members"></a>SQLServerPreparedStatement 成员
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出了通过公开的成员[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)类。  
  
## <a name="constructors"></a>构造函数  
 无。  
  
## <a name="fields"></a>字段  
 无。  
  
## <a name="inherited-fields"></a>继承的字段  
  
|类继承自：|方法|  
|---------------------------|-------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS、CLOSE_CURRENT_RESULT、EXECUTE_FAILED、KEEP_CURRENT_RESULT、NO_GENERATED_KEYS、RETURN_GENERATED_KEYS、SUCCESS_NO_INFO|  
  
## <a name="methods"></a>方法  
  
|Name|Description|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md)|将一组参数添加到此语句对象的命令的批处理。|  
|[取消](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)取消当前正在运行此语句对象的 SQL 语句。|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md)|此清空的 SQL 命令的当前列表[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。|  
|[clearParameters](../../../connect/jdbc/reference/clearparameters-method-sqlserverpreparedstatement.md)|立即清除当前参数值。|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)清除此语句对象报告的所有警告。|  
|[关闭](../../../connect/jdbc/reference/close-method-sqlserverpreparedstatement.md)|释放数据库和 JDBC 资源立即而不是等待它们自动释放此语句对象。|  
|[执行](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)|在此语句对象，它可以是任何类型的 SQL 语句中运行的 SQL 语句。|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverpreparedstatement.md)|向数据库提交要运行的命令批。 如果所有命令都成功运行，则返回一个更新计数数组。|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)|此语句对象中运行 SQL 查询并返回[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)由查询生成的对象。|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)|在此语句对象中，它必须是 SQL INSERT、 UPDATE、 MERGE 或 DELETE 语句; 运行的 SQL 语句或返回任何内容，例如 DDL 语句的 SQL 语句。|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)检索[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)生成此语句对象的对象。|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)检索从数据库表获取行的方向是从该语句对象生成的结果集的默认值。|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)检索此语句对象从生成的对象是结果的默认提取大小的结果集行数设置。|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)检索作为结果运行此语句对象创建的任何自动生成的密钥。|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)检索的最大可以为字符和二进制列中的值返回的字节数[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)此语句对象生成的对象。|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)检索最大行数， [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)可以包含此语句对象生成的对象。|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverpreparedstatement.md)|检索[SQLServerResultSetMetaData 类](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)对象，其中包含的列的信息[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)执行此语句对象时将返回的对象。|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)移动到此语句对象的下一个结果。|  
|[getParameterMetaData](../../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md)|检索数量、 类型和此语句对象的参数的属性。|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)检索此缓冲模式响应[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)检索的秒数[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]将等待运行此语句对象。|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)检索当前结果作为[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)检索结果集的并发性[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)此语句对象生成的对象。|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)检索结果集的保持能力[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)此语句对象生成的对象。|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)检索结果集类型[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)此语句对象生成的对象。|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)，) 检索当前结果以更新计数的形式。|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)检索此语句对象报告的调用的第一个警告。|  
|[关闭](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)指示是否已关闭此语句对象。|  
|[isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)返回指示是否可以将语句添加到用户提供的语句池的一个值。|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)|指示此语句对象是否为指定接口的包装。|  
|[setArray](../../../connect/jdbc/reference/setarray-method-sqlserverpreparedstatement.md)|将指定的参数号设置为给定的数组对象。|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)|将指定的参数号设置为给定的 InputStream 对象。|  
|[setBigDecimal](../../../connect/jdbc/reference/setbigdecimal-method-sqlserverpreparedstatement.md)|将指定的参数号设置为给定的 BigDecimal 对象。|  
|[setBinaryStream](../../../connect/jdbc/reference/setbinarystream-method-sqlserverpreparedstatement.md)|将指定参数设置为指定的输入流。|  
|[setBlob](../../../connect/jdbc/reference/setblob-method-sqlserverpreparedstatement.md)|将指定的参数设置为指定的 Blob 对象。|  
|[setboolean](../../../connect/jdbc/reference/setboolean-method-sqlserverpreparedstatement.md)|将指定的参数设置为指定**布尔**值。|  
|[setByte](../../../connect/jdbc/reference/setbyte-method-sqlserverpreparedstatement.md)|将指定的参数设置为指定**字节**值。|  
|[setBytes](../../../connect/jdbc/reference/setbytes-method-sqlserverpreparedstatement.md)|将指定参数设置为指定的字节数组。|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlserverpreparedstatement.md)|将指定的参数设置为指定的读取器对象。|  
|[setClob](../../../connect/jdbc/reference/setclob-method-sqlserverpreparedstatement.md)|将指定的参数设置为给定的 Clob 对象。|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)将 SQL 游标名称设置为指定字符串，此字符串将由后续的执行方法使用。|  
|[setDate](../../../connect/jdbc/reference/setdate-method-sqlserverpreparedstatement.md)|将指定参数设置为指定的日期值。|  
|[setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlserverpreparedstatement.md)|设置为指定的列的值[DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)值。|  
|[setDouble](../../../connect/jdbc/reference/setdouble-method-sqlserverpreparedstatement.md)|将指定的参数设置为指定**double**值。|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)设置转义处理模式。|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)为 JDBC 驱动程序提供提示以指明处理结果集行时应采用的方向。|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)为 JDBC 驱动程序提供提示以指明在需要更多行时应从数据库中提取的行数。|  
|[setFloat](../../../connect/jdbc/reference/setfloat-method-sqlserverpreparedstatement.md)|将指定的参数设置为指定**float**值。|  
|[setInt](../../../connect/jdbc/reference/setint-method-sqlserverpreparedstatement.md)|将指定的参数设置为指定**int**值。|  
|[setLong](../../../connect/jdbc/reference/setlong-method-sqlserverpreparedstatement.md)|将指定的参数设置为指定**长**值。|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)设置最大中的字节数的限制[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)存储字符或到给定的字节数的二进制值的列。|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)对任何设置的最大行数限制[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象可以包含到指定的数字。|  
|[setNCharacterStream](../../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)|将指定的参数设置为指定的读取器对象。|  
|[setNClob](../../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md)|将指定参数设置为指定对象。|  
|[setNull](../../../connect/jdbc/reference/setnull-method-sqlserverpreparedstatement.md)|根据要设置的参数的类型，将指定参数设置为 Null 值。|  
|[setNString](../../../connect/jdbc/reference/setnstring-method-int-java-lang-string.md)|将指定的参数设置为指定**字符串**对象。|  
|[setObject](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)|设置使用给定的对象的指定参数的值。|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)请求语句入池或不入池。 默认情况下，SQLServerPreparedStatement 对象是在创建时能合并。|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)设置驱动程序将等待语句对象若要运行到指定的秒数的秒数。|  
|[setRef](../../../connect/jdbc/reference/setref-method-sqlserverpreparedstatement.md)|将指定的参数设置为指定的 Ref 对象。|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|(继承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)设置此缓冲模式响应[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)到不区分大小写的对象**字符串完整**或**自适应**。|  
|[setShort](../../../connect/jdbc/reference/setshort-method-sqlserverpreparedstatement.md)|将指定的参数设置为指定**短**值。|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlserverpreparedstatement.md)|将指定的参数设置为指定**字符串**值。|  
|[setSQLXML](../../../connect/jdbc/reference/setsqlxml-method-sqlserverpreparedstatement.md)|将指定的参数设置为指定**SQLXML**对象。|  
|[setTime](../../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)|将指定参数设置为指定的 time 值。|  
|[setTimestamp](../../../connect/jdbc/reference/settimestamp-method-sqlserverpreparedstatement.md)|将指定参数设置为指定的 timestamp 值。|  
|[setUnicodeStream](../../../connect/jdbc/reference/setunicodestream-method-sqlserverpreparedstatement.md)|将指定的参数号设置为指定的输入流，其将具有指定的字节数。|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverpreparedstatement.md)|将指定参数设置为指定的 URL 值。|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)|返回一个实现指定的接口，以允许访问的对象[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]的特定方法。|  
  
## <a name="inherited-methods"></a>继承的方法  
  
|类继承自：|方法|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerStatement|cancel、clearWarnings、execute、executeUpdate、getConnection、getFetchDirection、getFetchSize、getGeneratedKeys、getMaxFieldSize、getMaxRows、getMoreResults、getQueryTimeout、getResultSet、getResultSetConcurrency、getResultSetHoldability、getResultSetType、getUpdateCount、getWarnings、isPoolable、setCursorName、setEscapeProcessing、setFetchDirection、setFetchSize、setMaxFieldSize、setMaxRows、setPoolable、setQueryTimeout|  
|java.lang.Object|clone、equals、getClass、hashCode、notify、notifyAll、toString、wait|  
|java.sql.Statement|cancel、clearWarnings、execute、executeUpdate、getConnection、getFetchDirection、getFetchSize、getGeneratedKeys、getMaxFieldSize、getMaxRows、getMoreResults、getQueryTimeout、getResultSet、getResultSetConcurrency、getResultSetHoldability、getResultSetType、getUpdateCount、getWarnings、setCursorName、setEscapeProcessing、setFetchDirection、setFetchSize、setMaxFieldSize、setMaxRows、setQueryTimeout|  
|java.sql.Wrapper|isWrapperFor、unwrap|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  

