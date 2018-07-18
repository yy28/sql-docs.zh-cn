---
title: SQLServerConnectionPoolDataSource 成员 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: dac0337e-8088-488c-a25a-801a2190f6ca
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dfebe1a58cb3a4e7f91d1395a875a705ef8f45db
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32852642"
---
# <a name="sqlserverconnectionpooldatasource-members"></a>SQLServerConnectionPoolDataSource 成员
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出了通过公开的成员[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)类。  
  
## <a name="constructors"></a>构造函数  
  
|名称|Description|  
|----------|-----------------|  
|[SQLServerConnectionPoolDataSource （)](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-constructor.md)|初始化的新实例[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)类。|  
  
## <a name="fields"></a>字段  
 无。  
  
## <a name="inherited-fields"></a>继承的字段  
 无。  
  
## <a name="methods"></a>方法  
  
|名称|Description|  
|----------|-----------------|  
|[getApplicationIntent](../../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 返回的值**applicationIntent**连接属性。|  
|[getApplicationName](../../../connect/jdbc/reference/getapplicationname-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 返回的应用程序名称。|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 尝试建立与此数据源对象表示的数据源的连接。|  
|[getDatabaseName](../../../connect/jdbc/reference/getdatabasename-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 返回的数据库名称。|  
|[getDescription](../../../connect/jdbc/reference/getdescription-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 返回的数据源的说明。|  
|[getFailoverPartner](../../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 返回数据库镜像配置中使用的故障转移服务器的名称。|  
|[getInstanceName](../../../connect/jdbc/reference/getinstancename-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 返回[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]实例名称。|  
|[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 返回**布尔**值，该值指示是否启用了 lastUpdateCount 属性。|  
|[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 返回**int**值，该值指示数据库将报告锁定超时之前等待的毫秒数。|  
|[getLoginTimeout](../../../connect/jdbc/reference/getlogintimeout-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 返回的此数据源对象将在尝试建立连接时等待的秒数。|  
|[getLogWriter](../../../connect/jdbc/reference/getlogwriter-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 返回可用于所有日志记录和跟踪消息的字符输出流。|  
|[getMultiSubnetFailover](../../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 返回的值**multiSubnetFailover**连接属性。|  
|[getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)|尝试建立可用作池连接的物理数据库连接。|  
|[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 返回用于与进行通信的当前端口号[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[getReference](../../../connect/jdbc/reference/getreference-method-sqlserverconnectionpooldatasource.md)|返回对此数据源对象的引用。|  
|[getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 返回用于创建使用此数据源对象的所有结果集的默认游标类型。|  
|[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 返回**布尔**值，该值指示是否启用发送到服务器以 UNICODE 格式的字符串参数。|  
|[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 返回正在运行的计算机的名称[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 返回用于连接到数据源的 URL。|  
|[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 返回用于连接数据源的用户名称。|  
|[getWorkstationID](../../../connect/jdbc/reference/getworkstationid-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 返回用于连接到数据源的计算机名称的客户端的名称。|  
|[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 返回**布尔**值，该值指示是否启用将 SQL 状态转换为 XOPEN 符合状态。|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)|指示此对象是否为指定接口的包装。|  
|[setApplicationIntent](../../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 设置的值**applicationIntent**连接属性。|  
|[setApplicationName](../../../connect/jdbc/reference/setapplicationname-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 设置应用程序名称。|  
|[setAuthenticationSceme](../../../connect/jdbc/reference/setauthenticationscheme-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 指示所需应用程序以使用集成安全性的类型。|  
|[setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 设置要连接到的数据库名称。|  
|[setDescription](../../../connect/jdbc/reference/setdescription-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 设置数据源的说明。|  
|[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 设置数据库镜像配置中使用的故障转移服务器的名称。|  
|[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 集[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]实例名称。|  
|[setIntegratedSecurity](../../../connect/jdbc/reference/setintegratedsecurity-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 集**布尔**值，该值指示是否启用了 integratedSecurity 属性。|  
|[setLastUpdateCount](../../../connect/jdbc/reference/setlastupdatecount-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 集**布尔**值，该值指示是否启用了 lastUpdateCount 属性。|  
|[setLockTimeout](../../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 集**int**值，该值指示在数据库报告锁定超时之前要等待的毫秒数。|  
|[setLoginTimeout](../../../connect/jdbc/reference/setlogintimeout-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 设置的此数据源对象将在尝试建立连接时等待的秒数。|  
|[setLogWriter](../../../connect/jdbc/reference/setlogwriter-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 设置可用于所有日志记录和跟踪消息的字符输出流。|  
|[setMultiSubnetFailover](../../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 设置的值**multiSubnetFailover**连接属性。|  
|[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 设置将用于连接到的密码[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 设置要用于与通信的端口号[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[setSelectMethod](../../../connect/jdbc/reference/setselectmethod-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 设置用于创建使用此数据源对象的所有结果集的默认游标类型。|  
|[setSendStringParametersAsUnicode](../../../connect/jdbc/reference/setsendstringparametersasunicode-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 集**布尔**值，该值指示是否启用发送到服务器以 UNICODE 格式的字符串参数。|  
|[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 设置为运行的计算机的名称[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 设置用于连接到数据源的 URL。|  
|[setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 设置用于连接数据源的用户名。|  
|[setWorkstationID](../../../connect/jdbc/reference/setworkstationid-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 设置的客户端用于连接到数据源的计算机名称。|  
|[setXopenStates](../../../connect/jdbc/reference/setxopenstates-method-sqlserverdatasource.md)|(继承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 集**布尔**值，该值指示是否启用将 SQL 状态转换为 XOPEN 符合状态。|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)|返回一个实现指定的接口，以允许访问的对象[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]的特定方法。|  
  
## <a name="inherited-methods"></a>继承的方法  
  
|类继承自：|方法|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerDataSource|getApplicationName、getConnection、getDatabaseName、getDescription、getFailoverPartner、getInstanceName、getLastUpdateCount、getLockTimeout、getLoginTimeout、getLogWriter、getPortNumber、getSelectMethod、getSendStringParametersAsUnicode、getServerName、getURL、getUser、getWorkstationID、getXopenStates、setApplicationName、setDatabaseName、setDescription、setFailoverPartner、setInstanceName、setIntegratedSecurity、setLastUpdateCount、setLockTimeout、setLoginTimeout、setLogWriter、setPassword、setPortNumber、setSelectMethod、setSendStringParametersAsUnicode、setServerName、setURL、setUser、setWorkstationID、setXopenStates|  
|java.lang.Object|clone、 equals、 finalize、 getClass、 hashCode、 notify、 notifyAll、 toString、 wait|  
|java.sql.Wrapper|isWrapperFor、unwrap|  
|javax.sql.ConnectionPoolDataSource|getLoginTimeout、getLogWriter、setLoginTimeout、setLogWriter、getPooledConnection|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerConnectionPoolDataSource 类](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
