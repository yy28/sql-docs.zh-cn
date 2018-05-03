---
title: SQLServerResultSet 成员 |Microsoft 文档
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
ms.assetid: 2a438d5d-2d6a-46a0-a2ae-f35fbae4a472
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 610ace1ea15f69277cba1e4bd37b365a2c3e1cc9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlserverresultset-members"></a>SQLServerResultSet 成员
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出了通过公开的成员[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)类。  
  
## <a name="constructors"></a>构造函数  
 无。  
  
## <a name="fields"></a>字段  
  
|名称|Description|  
|----------|-----------------|  
|[CONCUR_SS_OPTIMISTIC_CC](../../../connect/jdbc/reference/concur-ss-optimistic-cc-field-sqlserverresultset.md)|用于指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]读/写无行锁的开放式并发类型。|  
|[CONCUR_SS_OPTIMISTIC_CCVAL](../../../connect/jdbc/reference/concur-ss-optimistic-ccval-field-sqlserverresultset.md)|用于指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]读/写无行锁的开放式并发类型。|  
|[CONCUR_SS_SCROLL_LOCKS](../../../connect/jdbc/reference/concur-ss-scroll-locks-field-sqlserverresultset.md)|用于指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]读/写与行锁的开放式并发类型。|  
|[TYPE_SS_DIRECT_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-direct-forward-only-field-sqlserverresultset.md)|用于指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]快速只进、 只读游标类型。|  
|[TYPE_SS_SCROLL_DYNAMIC](../../../connect/jdbc/reference/type-ss-scroll-dynamic-field-sqlserverresultset.md)|用于指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]动态游标类型。|  
|[TYPE_SS_SCROLL_KEYSET](../../../connect/jdbc/reference/type-ss-scroll-keyset-field-sqlserverresultset.md)|用于指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]键集游标类型。|  
|[TYPE_SS_SCROLL_STATIC](../../../connect/jdbc/reference/type-ss-scroll-static-field-sqlserverresultset.md)|用于指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]静态游标类型。|  
|[TYPE_SS_SERVER_CURSOR_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-server-cursor-forward-only-field-sqlserverresultset.md)|用于指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]快速只进、 只读游标类型。|  
  
## <a name="inherited-fields"></a>继承的字段  
  
|类继承自：|Description|  
|---------------------------|-----------------|  
|java.sql.ResultSet|CLOSE_CURSORS_AT_COMMIT、CONCUR_READ_ONLY、CONCUR_UPDATABLE、FETCH_FORWARD、FETCH_REVERSE、FETCH_UNKNOWN、HOLD_CURSORS_OVER_COMMIT、TYPE_FORWARD_ONLY、TYPE_SCROLL_INSENSITIVE 和 TYPE_SCROLL_SENSITIVE|  
  
## <a name="methods"></a>方法  
  
|名称|Description|  
|----------|-----------------|  
|[绝对](../../../connect/jdbc/reference/absolute-method-sqlserverresultset.md)|将光标移到在此指定的行[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[afterLast](../../../connect/jdbc/reference/afterlast-method-sqlserverresultset.md)|最后一行后移动光标所在位置到[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[beforeFirst](../../../connect/jdbc/reference/beforefirst-method-sqlserverresultset.md)|光标会移动到此的第一行之前[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[cancelRowUpdates](../../../connect/jdbc/reference/cancelrowupdates-method-sqlserverresultset.md)|取消对当前行中所做的更新[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverresultset.md)|清除此报告的所有警告[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[关闭](../../../connect/jdbc/reference/close-method-sqlserverresultset.md)|释放此[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象的数据库和 JDBC 资源而等待自动关闭时执行此操作无需立即。|  
|[DeleteRow](../../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md)|删除当前行从此[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象在基础数据库中。|  
|[完成](../../../connect/jdbc/reference/finalize-method-sqlserverresultset.md)|显式关闭这[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[findColumn](../../../connect/jdbc/reference/findcolumn-method-sqlserverresultset.md)|检索在此指定的列名称的第一匹配列的索引[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[first](../../../connect/jdbc/reference/first-method-sqlserverresultset.md)|将光标移到的第一行[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[getArray](../../../connect/jdbc/reference/getarray-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为一个数组对象。|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)为 ASCII 字符流的对象。|  
|[getBigDecimal](../../../connect/jdbc/reference/getbigdecimal-method-sqlserverresultset.md)|检索此当前行中指定的列索引的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为 java.math.BigDecimal。|  
|[getBinaryStream](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为二进制流的未解释字节。|  
|[GetBlob](../../../connect/jdbc/reference/getblob-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为 Java 编程语言中的 Blob 对象。|  
|[GetBoolean](../../../connect/jdbc/reference/getboolean-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为**布尔**Java 编程语言中。|  
|[GetByte](../../../connect/jdbc/reference/getbyte-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为**字节**Java 编程语言中。|  
|[GetBytes](../../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为**字节**Java 编程语言中的数组。|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)作为 java.io.Reader 对象的对象。|  
|[getClob](../../../connect/jdbc/reference/getclob-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)作为 Clob 对象 Java 编程语言中的对象。|  
|[getConcurrency](../../../connect/jdbc/reference/getconcurrency-method-sqlserverresultset.md)|检索此并发模式[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[getCursorName](../../../connect/jdbc/reference/getcursorname-method-sqlserverresultset.md)|检索使用的 SQL 游标名称[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[getDate](../../../connect/jdbc/reference/getdate-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)作为 Java 编程语言中的 java.sql.Date 对象的对象。|  
|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)|检索的形式指定的列的值[DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)对象。|  
|[GetDouble](../../../connect/jdbc/reference/getdouble-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为**double** Java 编程语言中。|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverresultset.md)|检索此提取方向[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md)|检索此提取大小[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[GetFloat](../../../connect/jdbc/reference/getfloat-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为**float** Java 编程语言中。|  
|[getHoldability](../../../connect/jdbc/reference/getholdability-method-sqlserverresultset.md)|检索此保持能力[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[getInt](../../../connect/jdbc/reference/getint-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为**int** Java 编程语言中。|  
|[getLong](../../../connect/jdbc/reference/getlong-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为**长**Java 编程语言中。|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md)|检索数量、 类型和属性的这[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象的列。|  
|[getNCharacterStream](../../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)|检索指定列的当前行中的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为读取器对象。|  
|[getNClob](../../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md)|检索指定列的当前行中的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为**NClob** Java 编程语言中的对象。|  
|[getNString](../../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)|检索指定列的当前行中的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)以 Java 编程语言的字符串形式的对象。|  
|[GetObject](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md)|获取指定列的当前行中的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)作为 Java 编程语言中的对象的对象。|  
|[getRef](../../../connect/jdbc/reference/getref-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)作为 Java 编程语言中的 Ref 对象的对象。|  
|[GetRow](../../../connect/jdbc/reference/getrow-method-sqlserverresultset.md)|检索当前行号。|  
|[getShort](../../../connect/jdbc/reference/getshort-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为**短**Java 编程语言中。|  
|[getStatement](../../../connect/jdbc/reference/getstatement-method-sqlserverresultset.md)|检索[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)生成此对象[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[GetString](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为**字符串**Java 编程语言中。|  
|[getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md)|检索指定列的当前行中的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为**SQLXML**对象。|  
|[getTime](../../../connect/jdbc/reference/gettime-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)作为 Java 编程语言中的 java.sql.Time 对象的对象。|  
|[getTimestamp](../../../connect/jdbc/reference/gettimestamp-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)作为 Java 编程语言中的 java.sql.Timestamp 对象的对象。|  
|[GetType](../../../connect/jdbc/reference/gettype-method-sqlserverresultset.md)|检索此游标类型[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[getUnicodeStream](../../../connect/jdbc/reference/getunicodestream-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)为 Unicode 字符流的对象。|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverresultset.md)|检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)作为 URL 对象的对象。|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverresultset.md)|检索此报告的调用的第一个警告[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[InsertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md)|将插入行的内容插入到此[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象，并放入数据库。|  
|[isAfterLast](../../../connect/jdbc/reference/isafterlast-method-sqlserverresultset.md)|检索光标是否在此的最后一行之后[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[isBeforeFirst](../../../connect/jdbc/reference/isbeforefirst-method-sqlserverresultset.md)|检索光标是否在此第一行的前面[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[关闭](../../../connect/jdbc/reference/isclosed-method-sqlserverresultset.md)|指示是否这[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象已关闭。|  
|[isFirst](../../../connect/jdbc/reference/isfirst-method-sqlserverresultset.md)|检索光标所在的第一行是否[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[isLast](../../../connect/jdbc/reference/islast-method-sqlserverresultset.md)|检索光标是否位于此最后一行[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[最后一个](../../../connect/jdbc/reference/last-method-sqlserverresultset.md)|将光标移到中的最后一行[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[moveToCurrentRow](../../../connect/jdbc/reference/movetocurrentrow-method-sqlserverresultset.md)|将光标移到所记住的光标位置，通常为当前行。|  
|[moveToInsertRow](../../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md)|将游标移到插入行。|  
|[下一步](../../../connect/jdbc/reference/next-method-sqlserverresultset.md)|将游标从当前位置下移一行。|  
|[上一个](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md)|将光标移至前一行中这[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[refreshRow](../../../connect/jdbc/reference/refreshrow-method-sqlserverresultset.md)|使用数据库中当前行的最新值刷新此行。|  
|[relative](../../../connect/jdbc/reference/relative-method-sqlserverresultset.md)|将光标沿正向或反向移动相对于当前行的指定行数。|  
|[RowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md)|检索是否已删除某行。|  
|[rowInserted](../../../connect/jdbc/reference/rowinserted-method-sqlserverresultset.md)|检索当前行是否曾插入内容。|  
|[RowUpdated](../../../connect/jdbc/reference/rowupdated-method-sqlserverresultset.md)|检索当前行是否已更新。|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md)|在其中提供有关方向提示中行[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)将处理对象。|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md)|提供有关此需要更多的行时应从数据库提取的行数的提示的 JDBC 驱动程序[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[updateArray](../../../connect/jdbc/reference/updatearray-method-sqlserverresultset.md)|使用一个数组对象中更新指定的列。|  
|[updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)|使用 ASCII 流值更新指定列。|  
|[updateBigDecimal](../../../connect/jdbc/reference/updatebigdecimal-method-sqlserverresultset.md)|更新与 BigDecimal 对象指定的列。|  
|[updateBinaryStream](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)|使用二进制流值更新指定列。|  
|[updateBlob](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)|使用 java.sql.Blob 值更新指定列。|  
|[updateBoolean](../../../connect/jdbc/reference/updateboolean-method-sqlserverresultset.md)|更新的指定的列**布尔**值。|  
|[updateByte](../../../connect/jdbc/reference/updatebyte-method-sqlserverresultset.md)|更新的指定的列**字节**值。|  
|[updateBytes](../../../connect/jdbc/reference/updatebytes-method-sqlserverresultset.md)|会将指定的列更新的数组**字节**值。|  
|[updateCharacterStream](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)|使用字符流值更新指定列。|  
|[updateClob](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)|使用 java.sql.Clob 值更新指定列。|  
|[updateDate](../../../connect/jdbc/reference/updatedate-method-sqlserverresultset.md)|使用日期值更新指定列。|  
|[updateDateTimeOffset](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md)|更新[DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)列。|  
|[updateDouble](../../../connect/jdbc/reference/updatedouble-method-sqlserverresultset.md)|更新的指定的列**double**值。|  
|[updateFloat](../../../connect/jdbc/reference/updatefloat-method-sqlserverresultset.md)|更新的指定的列**float**值。|  
|[updateInt](../../../connect/jdbc/reference/updateint-method-sqlserverresultset.md)|更新的指定的列**int**值。|  
|[updateLong](../../../connect/jdbc/reference/updatelong-method-sqlserverresultset.md)|更新的指定的列**长**值。|  
|[updateNCharacterStream](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)|使用字符流值更新指定列。|  
|[updateNClob](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)|使用指定对象值更新指定列。|  
|[updateNString](../../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)|更新的指定的列**字符串**值。|  
|[updateNull](../../../connect/jdbc/reference/updatenull-method-sqlserverresultset.md)|使用 Null 值更新指定列。|  
|[updateObject](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)|更新的指定的列**对象**值。|  
|[updateRef](../../../connect/jdbc/reference/updateref-method-sqlserverresultset.md)|使用 java.sql.Ref 值更新指定列。|  
|[UpdateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md)|使用的当前行的新内容更新基础数据库[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[updateShort](../../../connect/jdbc/reference/updateshort-method-sqlserverresultset.md)|更新的指定的列**短**值。|  
|[updateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md)|更新的指定的列**字符串**值。|  
|[updateSQLXML](../../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md)|更新的指定的列**SQLXML**值。|  
|[updateTime](../../../connect/jdbc/reference/updatetime-method-sqlserverresultset.md)|使用时间值更新指定列。|  
|[updateTimestamp](../../../connect/jdbc/reference/updatetimestamp-method-sqlserverresultset.md)|使用时间戳的值更新指定列。|  
|[wasNull](../../../connect/jdbc/reference/wasnull-method-sqlserverresultset.md)|验证读取的最后一个值是否是一个 null 值。|  
  
## <a name="inherited-methods"></a>继承的方法  
  
|类继承自：|方法|  
|---------------------------|-------------|  
|java.lang.Object|clone、equals、getClass、hashCode、notify、notifyAll、toString、wait|  
|java.sql.Wrapper|isWrapperFor、unwrap|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
