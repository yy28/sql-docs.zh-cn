---
title: SQLServerStatement 成员 |Microsoft 文档
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
ms.assetid: 828cbaa9-ea7a-4986-95c3-5ba0d7d01d83
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 07071e2e84736ba7014c72e62f054af3829c4458
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlserverstatement-members"></a>SQLServerStatement 成员
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出了通过公开的成员[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)类。  
  
## <a name="constructors"></a>构造函数  
 无。  
  
## <a name="fields"></a>字段  
 无。  
  
## <a name="inherited-fields"></a>继承的字段  
  
|名称|Description|  
|----------|-----------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS、CLOSE_CURRENT_RESULT、EXECUTE_FAILED、KEEP_CURRENT_RESULT、NO_GENERATED_KEYS、RETURN_GENERATED_KEYS、SUCCESS_NO_INFO|  
  
## <a name="methods"></a>方法  
  
|名称|Description|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverstatement.md)|将给定的 SQL 命令添加到的命令的当前列表，此[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。|  
|[cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|取消当前正在此运行的 SQL 语句[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverstatement.md)|此清空的 SQL 命令的当前列表[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|清除此报告的所有警告[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。|  
|[关闭](../../../connect/jdbc/reference/close-method-sqlserverstatement.md)|释放此[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象的数据库和 JDBC 资源立即而不是等待它们自动释放。|  
|[execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)|运行可返回多个结果的给定的 SQL 语句。|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md)|向数据库提交要运行的命令批。 如果所有命令都成功运行，则返回一个更新计数数组。|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)|运行给定的 SQL 语句并返回单个[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)|运行给定的 SQL 语句，可以是 INSERT、UPDATE、MERGE 或 DELETE 语句；或不返回任何内容的 SQL 语句，例如 SQL DDL 语句。|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|检索[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)生成此对象[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|从数据库表提取行是从生成结果集的默认值为检索方向[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|检索的结果数设置为结果集生成从该对象是默认提取大小的行数[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|检索作为结果运行此命令创建的任何自动生成的密钥[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|检索的最大可以为字符和二进制列中的值返回的字节数[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)由此产生的对象[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|检索最大行数， [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)由此产生的对象[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象可以包含。|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|将移动到下一个结果此[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|检索的秒数[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]将等待对此[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象能够运行。|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|检索此缓冲模式响应[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|检索当前结果作为[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|检索结果集的并发性[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)此生成的对象[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|检索结果集的保持能力[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)此生成的对象[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|检索结果集类型[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)此生成的对象[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|检索当前结果作为更新计数。|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|检索此报告的调用的第一个警告[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。|  
|[关闭](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|指示是否这[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象已关闭。|  
|[isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|返回指示是否可以将语句添加到用户提供的语句池的一个值。|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)|指示此语句对象是否为指定接口的包装。|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|将 SQL 游标名称设置为给定字符串，该字符串将由随后的执行方法使用。|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|设置转义处理模式。|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|为 JDBC 驱动程序提供提示以指明处理结果集行时应采用的方向。|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|为 JDBC 驱动程序提供提示以指明在需要更多行时应从数据库中提取的行数。|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|设置最大中的字节数的限制[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)存储字符或到给定的字节数的二进制值的列。|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|对任何设置的最大行数限制[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象可以包含到指定的数字。|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|请求语句入池或不入池。|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|设置驱动程序将等待的秒数[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象，若要运行到指定的秒数。|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|设置此缓冲模式响应[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)到不区分大小写的对象**字符串完整**或**自适应**。|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)|返回一个实现指定的接口，以允许访问的对象[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]的特定方法。|  
  
## <a name="inherited-methods"></a>继承的方法  
  
|类继承自：|方法|  
|---------------------------|-------------|  
|java.lang.Object|clone、equals、getClass、hashCode、notify、notifyAll、toString、wait|  
|java.sql.Wrapper|isWrapperFor、unwrap|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
