---
title: "SQLServerConnection 成员 |Microsoft 文档"
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
ms.assetid: 3115a533-756b-4c78-aee9-4ba7253c85e0
caps.latest.revision: "25"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ac235e229d5156895c45d3e0ec705d0c2b84ca06
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="sqlserverconnection-members"></a>SQLServerConnection 成员
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出了通过公开的成员[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)类。  
  
## <a name="constructors"></a>构造函数  
 无。  
  
## <a name="fields"></a>字段  
  
|Name|Description|  
|----------|-----------------|  
|[TRANSACTION_SNAPSHOT](../../../connect/jdbc/reference/transaction-snapshot-field-sqlserverconnection.md)|用来指定快照事务隔离级别。|  
  
## <a name="inherited-fields"></a>继承的字段  
  
|类继承自：|Description|  
|---------------------------|-----------------|  
|java.sql.Connection|TRANSACTION_NONE、TRANSACTION_READ_COMMITTED、TRANSACTION_READ_UNCOMMITTED、TRANSACTION_REPEATABLE_READ、 TRANSACTION_SERIALIZABLE|  
  
## <a name="methods"></a>方法  
  
|Name|Description|  
|----------|-----------------|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverconnection.md)|清除此报告的所有警告[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象。|  
|[关闭](../../../connect/jdbc/reference/close-method-sqlserverconnection.md)|此释放数据库[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象和立即而不是等待它们自动释放的 JDBC 资源。|  
|[提交](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md)|进行所有更改以来所做的上一次提交或回滚永久性的并释放当前持有此任何数据库锁[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象。|  
|[createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md)|创建**java.sql.Blob**不包含任何数据的对象。|  
|[createClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md)|创建**java.sql.Clob**不包含任何数据的对象。|  
|[createNClob](../../../connect/jdbc/reference/createnclob-method-sqlserverconnection.md)|创建**java.sql.NClob**不包含任何数据的对象。|  
|[createStatement](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)|创建[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)发送到数据库的 SQL 语句的对象。|  
|[createSQLXML](../../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md)|创建**java.sql.SQLXML**不包含任何数据的对象。|  
|[getAutoCommit](../../../connect/jdbc/reference/getautocommit-method-sqlserverconnection.md)|检索当前的自动提交模式此[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象。|  
|[getCatalog](../../../connect/jdbc/reference/getcatalog-method-sqlserverconnection.md)|检索此的当前目录名称[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象。|  
|[getClientConnectionID 方法 &#40;SQLServerConnection &#41;](../../../connect/jdbc/reference/getclientconnectionid-method-sqlserverconnection.md)|无论最新连接尝试成功还是失败，都获取该尝试的连接 ID。|  
|[getClientInfo](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)|检索有关 JDBC 驱动程序支持的客户端信息属性信息。|  
|[getHoldability](../../../connect/jdbc/reference/getholdability-method-sqlserverconnection.md)|检索的当前保持能力[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)创建使用此对象[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象。|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md)|检索[SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)对象，其中包含有关此数据库的元数据[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象表示的连接。|  
|[getTransactionIsolation](../../../connect/jdbc/reference/gettransactionisolation-method-sqlserverconnection.md)|检索此当前事务的隔离级别[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象。|  
|[getTypeMap](../../../connect/jdbc/reference/gettypemap-method-sqlserverconnection.md)|检索与此关联的映射对象[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象。|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md)|检索此报告的调用的第一个警告[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象。|  
|[关闭](../../../connect/jdbc/reference/isclosed-method-sqlserverconnection.md)|指示是否这[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象已关闭。|  
|[isReadOnly](../../../connect/jdbc/reference/isreadonly-method-sqlserverconnection.md)|指示是否这[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象处于只读模式。|  
|[isValid](../../../connect/jdbc/reference/isvalid-method-sqlserverconnection.md)|指示是否这[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象未关闭，并且仍然有效。|  
|[nativeSQL](../../../connect/jdbc/reference/nativesql-method-sqlserverconnection.md)|将给定的 SQL 语句转换为数据库服务器的本机 SQL 语法。|  
|[prepareCall](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)|创建[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)调用数据库存储过程的对象。|  
|[prepareStatement](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)|创建[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)发送的对象参数化到数据库的 SQL 语句。|  
|[releaseSavepoint](../../../connect/jdbc/reference/releasesavepoint-method-sqlserverconnection.md)|中移除指定[SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md)从当前事务的对象。|  
|[回滚](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)|取消在当前事务中所做的所有更改并释放当前持有这任何数据库锁[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象。|  
|[setAutoCommit](../../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md)|此设置自动提交模式[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)到给定状态的对象。|  
|[setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md)|设置要选择这些子空间的指定的目录名称[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)要在其中工作的对象的数据库。|  
|[setClientInfo](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)|设置客户端信息属性的值。|  
|[setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md)|更改的保持能力[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)创建使用此对象[SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md)到给定的保持能力的对象。|  
|[setReadOnly](../../../connect/jdbc/reference/setreadonly-method-sqlserverconnection.md)|将此[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)在只读模式下的 JDBC 驱动程序，若要启用数据库优化提示的对象。|  
|[setSavepoint](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)|当前事务中创建未命名的保存点并返回新[SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md)表示它的对象。|  
|[setTransactionIsolation](../../../connect/jdbc/reference/settransactionisolation-method-sqlserverconnection.md)|尝试将事务隔离级别更改此[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)到给定的对象。|  
|[setTypeMap](../../../connect/jdbc/reference/settypemap-method-sqlserverconnection.md)|将给定的 TypeMap 对象的类型映射作为安装此[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象。|  
  
## <a name="inherited-methods"></a>继承的方法  
  
|类继承自：|方法|  
|---------------------------|-------------|  
|java.lang.Object|clone、 equals、 finalize、 getClass、 hashCode、 notify、 notifyAll、 toString、 wait|  
|java.lang.Wrapper|isWrapperFor、unwrap|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
