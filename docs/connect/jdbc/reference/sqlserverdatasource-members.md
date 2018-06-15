---
title: SQLServerDataSource 成员 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7e749bc5-d765-4864-be2b-7822d4c20c09
caps.latest.revision: 43
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 52f0cd9f341e7bc2ee4c45997542057d7e32983d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853052"
---
# <a name="sqlserverdatasource-members"></a>SQLServerDataSource 成员
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出了通过公开的成员[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)类。  
  
## <a name="constructors"></a>构造函数  
  
|名称|Description|  
|----------|-----------------|  
|[SQLServerDataSource （)](../../../connect/jdbc/reference/sqlserverdatasource-constructor.md)|初始化的新实例[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)类。|  
  
## <a name="fields"></a>字段  
 无。  
  
## <a name="inherited-fields"></a>继承的字段  
 无。  
  
## <a name="methods"></a>方法  
  
|名称|Description|  
|----------|-----------------|  
|[getApplicationIntent](../../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)|返回的值**applicationIntent**连接属性。|  
|[getApplicationName](../../../connect/jdbc/reference/getapplicationname-method-sqlserverdatasource.md)|返回应用程序名称。|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)|尝试建立连接的数据源此[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)对象所表示。|  
|[getDatabaseName](../../../connect/jdbc/reference/getdatabasename-method-sqlserverdatasource.md)|返回数据库名称。|  
|[getDisableStatementPooling](../../../connect/jdbc/reference/getdisablestatementpooling-method-sqlserverdatasource.md)|返回的值**disableStatementPooling**连接属性。 此设置可控制是否启用语句池或不适用于此连接。|  
|[getEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/getenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource.md)|返回的值**enablePrepareOnFirstPreparedStatementCall**连接属性。|  
|[getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md)|返回**布尔**值，该值指示是否启用加密属性。|  
|[getDescription](../../../connect/jdbc/reference/getdescription-method-sqlserverdatasource.md)|返回数据源的说明。|  
|[getFailoverPartner](../../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)|返回在数据库镜像配置中使用的故障转移服务器名称。|  
|[getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md)|返回用于验证 SQL Server 安全套接字层 (SSL) 证书的主机名。|  
|[getInstanceName](../../../connect/jdbc/reference/getinstancename-method-sqlserverdatasource.md)|返回[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]实例名称。|  
|[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)|返回**布尔**值，该值指示是否启用 lastUpdateCount 属性。|  
|[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md)|返回**int**值，该值指示数据库报告锁定超时之前等待的毫秒数。|  
|[getLoginTimeout](../../../connect/jdbc/reference/getlogintimeout-method-sqlserverdatasource.md)|返回的秒数这[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)尝试建立连接时等待对象。|  
|[getLogWriter](../../../connect/jdbc/reference/getlogwriter-method-sqlserverdatasource.md)|返回用于所有日志记录和跟踪消息的字符输出流。|  
|[getMultiSubnetFailover](../../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)|返回的值**multiSubnetFailover**连接属性。|  
|[getPacketSize](../../../connect/jdbc/reference/getpacketsize-method-sqlserverdatasource.md)|返回用于与进行通信的当前网络数据包大小[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]，以字节为单位指定。|  
|[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md)|返回用于与进行通信的当前端口号[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[getReference](../../../connect/jdbc/reference/getreference-method-sqlserverdatasource.md)|返回对此引用[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)对象。|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverdatasource.md)|返回此缓冲模式响应[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)对象。|  
|[getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)|返回用于使用此创建的所有结果集的默认游标类型[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)对象。|  
|[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md)|返回**布尔**值，该值指示是否启用发送到服务器以 UNICODE 格式的字符串参数。|  
|[getSendTimeAsDatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md)|返回的设置**SendTimeAsDatetime**连接属性。|  
|[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md)|返回运行的计算机的名称[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[getServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/getserverpreparedstatementdiscardthreshold-method-sqlserverdatasource.md)|返回的值**serverPreparedStatementDiscardThreshold**连接属性。|  
|[getStatementPoolingCacheSize](../../../connect/jdbc/reference/getstatementpoolingcachesize-method-sqlserverdatasource.md)|返回此连接的已准备的语句缓存的大小。|  
|[getTrustManagerClass](../../../connect/jdbc/reference/gettrustmanagerclass-method-sqlserverdatasource.md)|返回 TrustManagerClass 连接属性的字符串值。|  
|[getTrustManagerConstructorArg](../../../connect/jdbc/reference/gettrustmanagerconstructorarg-method-sqlserverdatasource.md)|返回 TrustManagerConstructorArg 连接属性的字符串值。|  
|[getTrustServerCertificate](../../../connect/jdbc/reference/gettrustservercertificate-method-sqlserverdatasource.md)|返回**布尔**值，该值指示是否启用 trustServerCertificate 属性。|  
|[getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md)|返回指向证书 trustStore 文件的路径（包括文件名）。|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)|返回用于连接到数据源的 URL。|  
|[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md)|返回用来连接数据源的用户名称。|  
|[getUseSQLServerBaseDate](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md)|返回 useSQLServerBaseDate 连接属性的设置。|  
|[getWorkstationID](../../../connect/jdbc/reference/getworkstationid-method-sqlserverdatasource.md)|返回用于连接数据源的客户端计算机名。|  
|[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)|返回**布尔**值，该值指示是否启用将 SQL 状态转换为 XOPEN 符合状态。|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)|指示此数据源对象是否为指定接口的包装。|  
|[setApplicationIntent](../../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)|设置的值**applicationIntent**连接属性。|  
|[setApplicationName](../../../connect/jdbc/reference/setapplicationname-method-sqlserverdatasource.md)|设置应用程序名称。|  
|[setAuthenticationScheme](../../../connect/jdbc/reference/setauthenticationscheme-sqlserverdatasource.md)|指示您的应用程序要使用的集成安全性类型。|  
|[setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)|设置要连接到的数据库名称。|  
|[setDescription](../../../connect/jdbc/reference/setdescription-method-sqlserverdatasource.md)|设置数据源的说明。|  
|[setDisableStatementPooling](../../../connect/jdbc/reference/setdisablestatementpooling-method-sqlserverdatasource.md)|设置为 true 或 false 池语句。|  
|[setEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/setenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource.md)|指定的新值**enablePrepareOnFirstPreparedStatementCall**连接属性。|  
|[setEncrypt](../../../connect/jdbc/reference/setencrypt-method-sqlserverdatasource.md)|集**布尔**值，该值指示是否启用加密属性。|  
|[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)|设置在数据库镜像配置中使用的故障转移服务器名称。|  
|[setHostNameInCertificate](../../../connect/jdbc/reference/sethostnameincertificate-method-sqlserverdatasource.md)|设置要用于验证 SQL Server 安全套接字层 (SSL) 证书的主机名。|  
|[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)|集[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]实例名称。|  
|[setIntegratedSecurity](../../../connect/jdbc/reference/setintegratedsecurity-method-sqlserverdatasource.md)|集**布尔**值，该值指示是否启用 integratedSecurity 属性。|  
|[setLastUpdateCount](../../../connect/jdbc/reference/setlastupdatecount-method-sqlserverdatasource.md)|集**布尔**值，该值指示是否启用 lastUpdateCount 属性。|  
|[setLockTimeout](../../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md)|集**int**值，该值指示在数据库报告锁定超时之前要等待的毫秒数。|  
|[setLoginTimeout](../../../connect/jdbc/reference/setlogintimeout-method-sqlserverdatasource.md)|集的秒数的这[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)尝试建立连接时等待对象。|  
|[setLogWriter](../../../connect/jdbc/reference/setlogwriter-method-sqlserverdatasource.md)|设置用于所有日志记录和跟踪消息的字符输出流。|  
|[setMultiSubnetFailover](../../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)|设置的值**multiSubnetFailover**连接属性。|  
|[setPacketSize](../../../connect/jdbc/reference/setpacketsize-method-sqlserverdatasource.md)|设置用于与进行通信的当前网络数据包大小[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]，以字节为单位指定。|  
|[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)|设置用于连接到的密码[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)|设置用于与进行通信的端口号[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)|设置响应缓冲模式创建使用此连接[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)对象。|  
|[setSelectMethod](../../../connect/jdbc/reference/setselectmethod-method-sqlserverdatasource.md)|设置用于创建使用此的所有结果集的默认游标类型[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)对象。|  
|[setSendStringParametersAsUnicode](../../../connect/jdbc/reference/setsendstringparametersasunicode-method-sqlserverdatasource.md)|集**布尔**值，该值指示是否启用发送到服务器以 UNICODE 格式的字符串参数。|  
|[setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)|指定如何将 java.sql.Time 值发送到服务器。|  
|[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)|设置运行的计算机的名称[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[setServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/setserverpreparedstatementdiscardthreshold-method-sqlserverdatasource.md)|设置的新值**serverPreparedStatementDiscardThreshold**连接属性。|  
|[setStatementPoolingCacheSize](../../../connect/jdbc/reference/setstatementpoolingcachesize-method-sqlserverdatasource.md)|设置此连接的已准备的语句缓存的大小。|  
|[setTrustManagerClass](../../../connect/jdbc/reference/settrustmanagerclass-method-sqlserverdatasource.md)|设置 TrustManagerClass 连接属性的字符串值。|  
|[setTrustManagerConstructorArg](../../../connect/jdbc/reference/settrustmanagerconstructorarg-method-sqlserverdatasource.md)|设置 TrustManagerConstructorArg 连接属性的字符串值。|  
|[setTrustServerCertificate](../../../connect/jdbc/reference/settrustservercertificate-method-sqlserverdatasource.md)|集**布尔**值，该值指示是否启用 trustServerCertificate 属性。|  
|[setTrustStore](../../../connect/jdbc/reference/settruststore-method-sqlserverdatasource.md)|设置指向证书 trustStore 文件的路径（包括文件名）。|  
|[setTrustStorePassword](../../../connect/jdbc/reference/settruststorepassword-method-sqlserverdatasource.md)|设置用于检查 trustStore 数据完整性的密码。|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)|设置用于连接数据源的 URL。|  
|[setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)|设置用于连接数据源的用户名。|  
|[setWorkstationID](../../../connect/jdbc/reference/setworkstationid-method-sqlserverdatasource.md)|设置用于连接数据源的客户端计算机名。|  
|[setXopenStates](../../../connect/jdbc/reference/setxopenstates-method-sqlserverdatasource.md)|集**布尔**值，该值指示是否启用将 SQL 状态转换为 XOPEN 符合状态。|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)|返回一个实现指定的接口，以允许访问的对象[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]的特定方法。|  
  
## <a name="inherited-methods"></a>继承的方法  
  
|类继承自：|方法|  
|---------------------------|-------------|  
|java.lang.Object|clone、 equals、 finalize、 getClass、 hashCode、 notify、 notifyAll、 toString、 wait|  
|java.sql.Wrapper|isWrapperFor、unwrap|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
