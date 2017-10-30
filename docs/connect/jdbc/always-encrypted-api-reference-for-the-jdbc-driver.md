---
title: "始终加密的 JDBC 驱动程序的 API 参考 |Microsoft 文档"
ms.custom: 
ms.date: 11/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6962a2aa-9508-4d4f-a78c-905e2bc68615
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 008db0dabc1b0488daaef63945442b666ee02fa1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/27/2017

---
# <a name="always-encrypted-api-reference-for-the-jdbc-driver"></a>始终加密的 JDBC 驱动程序的 API 参考
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  始终加密允许客户端对客户端应用程序内的敏感数据进行加密，并且永远不向 SQL Server 显示加密密钥。 安装在客户端计算机上的启用始终加密的驱动程序通过在 SQL Server 客户端应用程序中对敏感数据进行加密和解密来实现此目标。 该驱动程序先对敏感列中的数据进行加密，然后再将该数据传递到 SQL Server，并且自动重写查询以便保留应用程序的语义。 同样，该驱动程序以透明方式对存储在加密数据库列（包含在查询结果中）中的数据进行解密。 有关详细信息，请参阅[始终加密 （数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)和[Using Always Encrypted with JDBC 驱动程序](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  始终加密功能支持的 Microsoft JDBC Driver 6.0 或更高版本的 SQL Server 2016 的 SQL Server。  
  
 对 JDBC 驱动程序 API 有多次新的添加和修改，以供在使用始终加密的客户端应用程序中使用。  
  
 **SQLServerConnection 类**  
  
|Name|说明|  
|----------|-----------------|  
|新的连接字符串关键字：<br /><br /> columnEncryptionSetting|columnEncryptionSetting = 已启用启用始终加密功能的连接和 columnEncryptionSetting = 已禁用禁用它。 接受的值为“启用”/“禁用”。 默认值为“禁用”。|  
|新方法：<br /><br /> 公共静态 void setColumnEncryptionTrustedMasterKeyPaths (映射 < 字符串，则列表\<字符串 >> trustedKeyPaths)<br /><br /> 公共静态 void updateColumnEncryptionTrustedMasterKeyPaths (字符串服务器，列表\<字符串 > trustedKeyPaths)<br /><br /> 公共静态 void removeColumnEncryptionTrustedMasterKeyPaths (字符串 server)|允许你为集/更新/删除的受信任密钥路径列表的数据库服务器。 如果在处理应用程序查询时，驱动程序收到不在列表上的密钥路径，则查询将失败。 此属性提供针对安全攻击的额外保护，这些攻击涉及到提供伪造密钥路径的受损 SQL Server，这可能导致泄露密钥存储凭据。|  
|新方法：<br /><br /> 公共静态映射 < 字符串，则列表\<字符串 >> getColumnEncryptionTrustedMasterKeyPaths()|为数据库服务器返回受信任的密钥路径的列表。|  
|新方法：<br /><br /> 公共静态 void registerColumnEncryptionKeyStoreProviders (映射\<字符串、 SQLServerColumnEncryptionKeyStoreProvider > clientKeyStoreProviders)|允许你注册自定义密钥存储提供程序。 它是一个将密钥存储提供程序名称映射到密钥存储提供程序实现的字典。<br /><br /> 若要使用 JVM 密钥存储，你需要使用 JVM 密钥存储凭据实例化 SQLServerColumnEncryptionJVMKeyStoreProvider 对象，并向驱动程序注册它。 为此提供程序名称必须是 MSSQL_JVM_KEYSTORE。<br /><br /> 若要使用 Azure 密钥保管库存储你需要实例化 SQLServerColumnEncryptionAzureKeyStoreProvider 对象并将它注册到该驱动程序。 为此提供程序名称必须是 AZURE_KEY_VAULT。|
|公共最终布尔 getSendTimeAsDatetime()|返回 sendTimeAsDatetime 连接属性的设置。|
|公共 void setSendTimeAsDatetime (布尔 sendTimeAsDateTimeValue)|修改 sendTimeAsDatetime 连接属性的设置。|

 **SQLServerConnectionPoolProxy 类**
|Name|Description|  
|----------|-----------------|  
|公共最终布尔 getSendTimeAsDatetime()|返回 sendTimeAsDatetime 连接属性的设置。|
|公共 void setSendTimeAsDatetime (布尔 sendTimeAsDateTimeValue)|修改 sendTimeAsDatetime 连接属性的设置。|
     
  
 **SQLServerDataSource 类**  
  
|Name|Description|  
|----------|-----------------|  
|公共 void setColumnEncryptionSetting (字符串 columnEncryptionSetting)|为数据源对象启用/禁用始终加密功能。<br /><br /> 默认值为“禁用”。|  
|公共字符串 getColumnEncryptionSetting()|检索数据源对象的始终加密功能设置。|
|公共 void setKeyStoreAuthentication (字符串 keyStoreAuthentication)|设置标识的密钥存储的名称。 支持的值是识别 Java 密钥存储"JavaKeyStorePassword"。<br/><br/>默认值为 null。|
|公共字符串 getKeyStoreAuthentication()|获取数据源对象的 keyStoreAuthentication 设置的值。|
|公共 void setKeyStoreSecret (字符串 keyStoreSecret)|设置 Java 密钥库的密码。 请注意，Java 密钥存储提供程序密钥库和密钥的密码必须相同。 请注意，必须使用"JavaKeyStorePassword"设置 keyStoreAuthentication。|
|公共 void setKeyStoreLocation (字符串 keyStoreLocation)|设置包括 Java 密钥库的文件名称的位置。 请注意，必须使用"JavaKeyStorePassword"设置 keyStoreAuthentication。|
|公共字符串 getKeyStoreLocation()|检索有关 Java 密钥存储 keyStoreLocation。|
  
 **SQLServerColumnEncryptionJavaKeyStoreProvider 类**  
  
 Java 密钥存储的密钥存储提供程序实现。 此类允许使用 Java 密钥库中存储为列主密钥的证书。  
  
 构造函数  
  
|Name|Description|  
|----------|-----------------|  
|公共 SQLServerColumnEncryptionJavaKeyStoreProvider （字符串 keyStoreLocation，char [] keyStoreSecret）|用于 Java 密钥存储的密钥存储提供程序。|  
  
 方法  
  
|Name|Description|  
|----------|-----------------|  
|公共字节 [] decryptColumnEncryptionKey （字符串 masterKeyPath、 字符串 encryptionAlgorithm、 字节 [] encryptedColumnEncryptionKey）|解密列加密密钥的指定加密值。 预期使用带有指定密钥路径的证书并使用指定算法加密该加密值。<br /><br /> **密钥路径的格式应为以下项之一：**<br /><br /> 指纹：<certificate_thumbprint><br /><br /> 别名：<certificate_alias><br /><br /> （重写 SQLServerColumnEncryptionKeyStoreProvider。 decryptColumnEncryptionKey （字符串、 字符串、 Byte[]).)|  
|公共字节 [] encryptColumnEncryptionKey （字符串 masterKeyPath、 字符串 encryptionAlgorithm、 字节 [] plainTextColumnEncryptionKey）|使用带有指定密钥路径的证书并使用指定算法加密列加密密钥。<br /><br /> **密钥路径的格式应为以下项之一：**<br /><br /> 指纹：<certificate_thumbprint><br /><br /> 别名：<certificate_alias><br /><br /> （重写 SQLServerColumnEncryptionKeyStoreProvider。 encryptColumnEncryptionKey （字符串、 字符串、 Byte[]).)|  
|公共 void setName （字符串名称）|设置此密钥存储提供程序的名称。|
|公共字符串 getName （)|获取此密钥存储提供程序的名称。|
  
 **SQLServerColumnEncryptionAzureKeyVaultProvider 类**  
  
 Azure 密钥保管库的密钥存储提供程序实现。 此类，可使用 Azure 密钥保管库中存储为列主密钥的密钥。  
  
 构造函数  
  
|Name|Description|  
|----------|-----------------|  
|公共 SQLServerColumnEncryptionAzureKeyVaultProvider （SQLServerKeyVaultAuthenticationCallback authenticationCallback，ExecutorService executorService）|Azure 密钥保管库的密钥存储提供程序。  你需要提供 SQLServerKeyVaultAuthenticationCallback 接口以检索 Azure 密钥保管库中密钥的访问令牌的实现。|  
  
 方法  
  
|Name|Description|  
|----------|-----------------|  
|公共字节 [] decryptColumnEncryptionKey （字符串 masterKeyPath、 字符串 encryptionAlgorithm、 字节 [] encryptedColumnEncryptionKey）|解密列加密密钥的指定加密值。 加密的值预期应使用和进行加密指定的列键 IDmaster 键使用指定的算法。 <br />（重写 SQLServerColumnEncryptionKeyStoreProvider。 decryptColumnEncryptionKey （字符串、 字符串、 Byte[]).)|  
|公共字节 [] encryptColumnEncryptionKey （字符串 masterKeyPath、 字符串 encryptionAlgorithm、 字节 [] columnEncryptionKey）|对列加密密钥使用指定的列主密钥和使用指定的算法进行加密。 <br />（重写 SQLServerColumnEncryptionKeyStoreProvider。 encryptColumnEncryptionKey （字符串、 字符串、 Byte[]).)|  
|公共 void setName （字符串名称）|设置此密钥存储提供程序的名称。|
|公共字符串 getName （)|获取此密钥存储提供程序的名称。|  
  
  
 **SQLServerKeyVaultAuthenticationCallback 接口**  
  
 此接口包含用于 Azure 密钥保管库身份验证，这是由用户来实现的一个方法。  
  
 方法  
  
|Name|Description|  
|----------|-----------------|  
|公共字符串 getAccessToken （字符串机构、 字符串资源、 String scope）;|该方法所需中重写。 方法用于获取访问令牌向 Azure 密钥保管库。|  
  
 **SQLServerColumnEncryptionKeyStoreProvider 类**  
  
 扩展此类以实现自定义密钥存储提供程序。  
  
|Name|Description|  
|----------|-----------------|  
|SQLServerColumnEncryptionKeyStoreProvider|所有密钥存储提供程序的基类。 自定义提供程序必须从此类派生和重写其成员函数，然后注册它使用 SQLServerConnection。 registerColumnEncryptionKeyStoreProviders()。|  
  
 方法  
  
|Name|Description|  
|----------|-----------------|  
|public abstract byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)|用于解密列加密密钥的指定加密值的基类方法。 预期使用带有指定密钥路径的列主密钥并使用指定算法加密该加密值。|  
|public abstract byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[]  columnEncryptionKey)|用于使用带有指定密钥路径的列主密钥并使用指定算法加密列加密密钥的基类算法。|
|公共抽象 void setName （字符串名称）|设置此密钥存储提供程序的名称。|
|公共抽象字符串 getName()|获取此密钥存储提供程序的名称。|  
  
 中的新的或重载方法**SQLServerPreparedStatement**类  
  
|Name|Description|  
|----------|-----------------|  
|公共 void setBigDecimal (int parameterIndex，x，int 精度 BigDecimal int 缩放)<br /><br /> 公共 void setObject （int parameterIndex，对象 x、 int targetSqlType、 整数精度，int 小数位数）<br /><br /> 公共 void setObject （int parameterIndex，对象 x、 SQLType targetSqlType、 整数精度，整数小数位数）<br /><br /> 公共 void setTime （int parameterIndex，x，int 缩放 java.sql.Time）<br /><br /> 公共 void setTimestamp （int parameterIndex，x，int 缩放 java.sql.Timestamp） <br />公共 void setDateTimeOffset （int parameterIndex，x，int 缩放 microsoft.sql.DateTimeOffset）|这些方法将重载与精度或小数位数参数和 / 或以特定的数据类型，需要精度和小数位数信息支持始终加密。|  
|公共 void setMoney (int parameterIndex，BigDecimal x)<br /><br /> 公共 void setSmallMoney (int parameterIndex，BigDecimal x)<br /><br /> 公共 void setUniqueIdentifier （int parameterIndex，字符串 guid）<br /><br /> 公共 void setDateTime (int parameterIndex java.sql.Timestamp x)<br /><br /> 公共 void setSmallDateTime (int parameterIndex java.sql.Timestamp x)|这些方法将添加以支持始终加密的数据类型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime。 <br/><br/>请注意，用于将参数值发送到加密的 datetime2 列使用现有的 setTimestamp() 方法。 用于加密的日期时间和 smalldatetime 列的新方法 setDateTime() 和 setSmallDateTime() 分别使用。|  
|公共最终 void setBigDecimal （int parameterIndex，x，int 精度 BigDecimal，int 缩放，布尔 forceEncrypt）<br /><br /> 公共最终 void setMoney (int parameterIndex，x，布尔 forceEncrypt BigDecimal)<br /><br /> 公共最终 void setSmallMoney (int parameterIndex，x，布尔 forceEncrypt BigDecimal)<br /><br /> 公共最终 void setBoolean （int parameterIndex、 布尔 x、 布尔 forceEncrypt）<br /><br /> 公共最终 void setByte （int parameterIndex，x，布尔 forceEncrypt 字节）<br /><br /> 公共最终 void setBytes （int parameterIndex、 字节 x[]、 布尔 forceEncrypt）<br /><br /> 公共最终 void setUniqueIdentifier （int parameterIndex、 字符串 guid、 布尔 forceEncrypt）<br /><br /> 公共最终 void setDouble （int parameterIndex、 双线 x，布尔 forceEncrypt）<br /><br /> 公共最终 void setFloat （int parameterIndex、 float x、 布尔 forceEncrypt）<br /><br /> 公共最终 void setInt （int parameterIndex、 int 值、 布尔 forceEncrypt）<br /><br /> 公共最终 void setLong （int parameterIndex、 长时间 x、 布尔 forceEncrypt）<br /><br /> 公共最终 setObject （int parameterIndex，对象 x、 int targetSqlType、 整数精度、 布尔 forceEncrypt 的 int 小数位数）<br /><br /> 公共最终 void setObject （int parameterIndex，对象 x、 SQLType targetSqlType、 整数精度、 布尔 forceEncrypt 的整数小数位数）<br /><br /> 公共最终 void setShort （int parameterIndex、 短 x、 布尔 forceEncrypt）<br /><br /> 公共最终 void setString (int parameterIndex，字符串 str 布尔 forceEncrypt)<br /><br /> 公共最终 void setNString （int parameterIndex、 字符串值、 布尔 forceEncrypt）<br /><br /> 公共最终 void setTime (int parameterIndex，x，int 缩放 java.sql.Time 布尔 forceEncrypt)<br /><br /> 公共最终 void setTimestamp (int parameterIndex，x，int 缩放 java.sql.Timestamp 布尔 forceEncrypt)<br /><br /> 公共最终 void setDateTimeOffset (int parameterIndex，x，int 缩放 microsoft.sql.DateTimeOffset 布尔 forceEncrypt)<br /><br /> 公共最终 void setDateTime （int parameterIndex，x，布尔 forceEncrypt java.sql.Timestamp）<br /><br /> 公共最终 void setSmallDateTime （int parameterIndex，x，布尔 forceEncrypt java.sql.Timestamp）<br /><br /> 公共最终 void setDate (int parameterIndex，x，java.util.Calendar cal java.sql.Date 布尔 forceEncrypt)<br /><br /> 公共最终 void setTime (int parameterIndex，x，java.util.Calendar cal java.sql.Time 布尔 forceEncrypt)<br /><br /> 公共最终 void setTimestamp (int parameterIndex，x，java.util.Calendar cal java.sql.Timestamp 布尔 forceEncrypt)|将指定的参数设置为给定的 java 值。<br /><br /> 如果布尔 forceEncrypt 设置为 true，查询将仅当将参数设置标识列加密，对连接或语句上启用始终加密。<br /><br /> 如果布尔 forceEncrypt 设置为 false，该驱动程序不会强制对参数加密。|  
  
 中的新的或重载方法**SQLServerCallableStatement**类  
  
|Name|Description|  
|----------|-----------------|  
|公共 void registerOutParameter （int parameterIndex、 int sqlType、 int 精度、 int 缩放）<br /><br /> 公共 void registerOutParameter （int parameterIndex、 SQLType sqlType、 int 精度、 int 缩放）<br /><br /> 公共 void registerOutParameter （字符串 parameterName、 int sqlType、 int 精度、 int 缩放）<br /><br /> 公共 void registerOutParameter （字符串 parameterName、 SQLType sqlType、 int 精度、 int 缩放）<br />公共 void setBigDecimal （字符串 parameterName、 BigDecimal bd，int 精度、 int 缩放）<br /><br /> 公共 void setTime （字符串 parameterName、 java.sql.Time t、 int 缩放）<br /><br /> 公共 void setTimestamp （字符串 parameterName、 java.sql.Timestamp t、 int 缩放）<br /><br /> 公共 void setDateTimeOffset （字符串 parameterName、 microsoft.sql.DateTimeOffset t、 int 缩放）<br/><br/>公共最终 void setObject （字符串 sCol，对象 x、 int targetSqlType、 整数精度，int 小数位数）|这些方法将重载与精度或小数位数参数和 / 或以特定的数据类型，需要精度和小数位数信息支持始终加密。|  
|公共 void setDateTime (字符串 parameterName、 java.sql.Timestamp x)<br /><br /> 公共 void setSmallDateTime (字符串 parameterName、 java.sql.Timestamp x)<br /><br /> 公共 void setUniqueIdentifier （字符串参数名称，字符串 guid）<br /><br /> 公共 void setMoney （字符串 parameterName，BigDecimal bd）<br /><br /> 公共 void setSmallMoney （字符串 parameterName，BigDecimal bd）<br/><br/>公共时间戳 getDateTime （int 索引）<br/><br/>公共时间戳 getDateTime (字符串 sCol)<br/><br/>公共时间戳 getDateTime （int 索引，日历 cal）<br/><br/>公共时间戳 getSmallDateTime （int 索引）<br/><br/>公共时间戳 getSmallDateTime (字符串 sCol)<br/><br/>公共时间戳 getSmallDateTime （int 索引，日历 cal）<br/><br/>公共时间戳 getSmallDateTime （字符串名称，日历 cal）<br/><br/>公共 BigDecimal getMoney （int 索引）<br/><br/>公共 BigDecimal getMoney (字符串 sCol)<br/><br/>公共 BigDecimal getSmallMoney （int 索引）<br/><br/>公共 BigDecimal getSmallMoney (字符串 sCol)|这些方法将添加以支持始终加密的数据类型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime。 <br/><br/>请注意，用于将参数值发送到加密的 datetime2 列使用现有的 setTimestamp() 方法。 用于加密的日期时间和 smalldatetime 列的新方法 setDateTime() 和 setSmallDateTime() 分别使用。|  
|公共 void setObject （字符串参数名称、 Object o、 int n、 int m、 布尔 forceEncrypt）<br /><br /> 公共 void setObject （字符串参数名称、 对象 obj、 SQLType jdbcType、 int 缩放、 布尔 forceEncrypt）<br /><br /> 公共 void setDate (字符串 parameterName，x，日历 c java.sql.Date 布尔 forceEncrypt)<br /><br /> 公共 void setTime （字符串参数名称、 java.sql.Time t、 int 规模、 布尔 forceEncrypt）<br /><br /> 公共 void setTime (字符串 parameterName，x，日历 c java.sql.Time 布尔 forceEncrypt)<br /><br /> 公共 void setDateTime （字符串 parameterName，x，布尔 forceEncrypt java.sql.Timestamp）<br /><br /> 公共 void setDateTimeOffset （字符串参数名称、 microsoft.sql.DateTimeOffset t、 int 规模、 布尔 forceEncrypt）<br /><br /> 公共 void setSmallDateTime （字符串 parameterName，x，布尔 forceEncrypt java.sql.Timestamp）<br /><br /> 公共 void setTimestamp （字符串参数名称、 java.sql.Timestamp t、 int 规模、 布尔 forceEncrypt）<br /><br /> 公共 void setTimestamp （字符串 parameterName，x，布尔 forceEncrypt java.sql.Timestamp）<br /><br /> 公共 void setUniqueIdentifier （字符串参数名称、 guid 字符串、 布尔 forceEncrypt）<br /><br /> 公共 void setBytes （字符串 parameterName、 字节 [] b、 布尔 forceEncrypt）<br /><br /> 公共 void setByte （字符串 parameterName、 字节 b、 布尔 forceEncrypt）<br /><br /> 公共 void setString （字符串 parameterName、 字符串 s、 布尔 forceEncrypt）<br /><br /> （字符串 parameterName、 字符串值、 布尔 forceEncrypt） 的公共最终 void setNString<br /><br /> 公共 void setMoney （字符串 parameterName、 BigDecimal bd，布尔 forceEncrypt）<br /><br /> 公共 void setSmallMoney （字符串 parameterName、 BigDecimal bd，布尔 forceEncrypt）<br /><br /> 公共 void setBigDecimal （字符串 parameterName、 BigDecimal bd，int 精度、 int 缩放、 布尔 forceEncrypt）<br /><br /> 公共 void setDouble （字符串 parameterName、 双线 d，布尔 forceEncrypt）<br /><br /> 公共 void setFloat （字符串 parameterName、 float f、 布尔 forceEncrypt）<br /><br /> 公共 void setInt (字符串 parameterName、 int i，布尔 forceEncrypt)<br /><br /> 公共 void setLong （字符串 parameterName、 长时间 l、 布尔 forceEncrypt）<br /><br /> 公共 void setShort （字符串 parameterName、 短 s 整数、 布尔 forceEncrypt）<br /><br /> 公共 void setBoolean （字符串 parameterNames、 布尔值 b、 布尔 forceEncrypt）<br/><br/>公共 void setTimeStamp (字符串 sCol，x，日历 c java.sql.Timestamp 布尔 forceEncrypt)|将指定的参数设置为给定的 java 值。<br /><br /> 如果布尔 forceEncrypt 设置为 true，查询将仅当将参数设置标识列加密，对连接或语句上启用始终加密。<br /><br /> 如果布尔 forceEncrypt 设置为 false，该驱动程序不会强制对参数加密。|
 

 中的新的或重载方法**SQLServerResultSet**类  
  
|Name|Description|  
|----------|-----------------|  
|公共字符串 getUniqueIdentifier (int columnIndex)<br/><br/>公共字符串 getUniqueIdentifier (字符串 columnLabel)<br/><br/>   公共 java.sql.Timestamp getDateTime (int columnIndex) <br/><br/> 公共 java.sql.Timestamp getDateTime (字符串 columnName)   <br/><br/> 公共 java.sql.Timestamp getDateTime （int columnIndex，日历 cal）   <br/><br/>公共 java.sql.Timestamp getDateTime （字符串 colName，日历 cal）    <br/><br/>公共 java.sql.Timestamp getSmallDateTime (int columnIndex)    <br/><br/> 公共 java.sql.Timestamp getSmallDateTime (字符串 columnName)   <br/><br/> 公共 java.sql.Timestamp getSmallDateTime （int columnIndex，日历 cal）   <br/><br/> 公共 java.sql.Timestamp getSmallDateTime （字符串 colName，日历 cal）   <br/><br/>  公共 BigDecimal getMoney (int columnIndex)  <br/><br/> 公共 BigDecimal getMoney (字符串 columnName)   <br/><br/> 公共 BigDecimal getSmallMoney (int columnIndex)   <br/><br/>  公共 BigDecimal getSmallMoney (字符串 columnName)  <br/><br/>公共 void updateMoney (字符串 columnName，BigDecimal x)    <br/><br/>  公共 void updateSmallMoney (字符串 columnName，BigDecimal x)  <br/><br/>     公共 void updateDateTime (int 索引 java.sql.Timestamp x) <br/><br/> 公共 void updateSmallDateTime (int 索引 java.sql.Timestamp x) |这些方法将添加以支持始终加密的数据类型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime。 <br/><br/>请注意，用于更新加密的 datetime2 列使用现有的 updateTimestamp() 方法。 用于加密的日期时间和 smalldatetime 列的新方法 updateDateTime() 和 updateSmallDateTime() 分别使用。|
|公共 void updateBoolean （int 索引、 布尔 x、 布尔 forceEncrypt）  <br/><br/>  公共 void updateByte （int 索引，x，布尔 forceEncrypt 字节）  <br/><br/>  公共 void updateShort （int 索引、 短 x、 布尔 forceEncrypt）  <br/><br/> 公共 void updateInt （int 索引，x，布尔 forceEncrypt int）   <br/><br/>  公共 void updateLong （int 索引、 长时间 x、 布尔 forceEncrypt）  <br/><br/> 公共 void updateFloat （int 索引、 float x、 布尔 forceEncrypt）   <br/><br/> 公共 void updateDouble （int 索引、 双线 x，布尔 forceEncrypt）   <br/><br/> 公共 void updateMoney （int 索引，x，布尔 forceEncrypt BigDecimal）   <br/><br/>  公共 void updateMoney (字符串 columnName，x，布尔 forceEncrypt BigDecimal)  <br/><br/> 公共 void updateSmallMoney （int 索引，x，布尔 forceEncrypt BigDecimal）   <br/><br/>  公共 void updateSmallMoney (字符串 columnName，x，布尔 forceEncrypt BigDecimal)  <br/><br/> 公共 void updateBigDecimal （int 索引，x，整数精度 BigDecimal，整数缩放，布尔 forceEncrypt）   <br/><br/>  公共 void updateString （int columnIndex、 字符串 stringValue、 布尔 forceEncrypt）  <br/><br/>  公共 void updateNString （int columnIndex、 字符串 nString、 布尔 forceEncrypt）  <br/><br/>  公共 void updateNString （字符串 columnLabel、 字符串 nString、 布尔 forceEncrypt）  <br/><br/> 公共 void updateBytes （int 索引、 字节 x[]、 布尔 forceEncrypt）   <br/><br/>  公共 void updateDate （int 索引，x，布尔 forceEncrypt java.sql.Date）  <br/><br/> 公共 void updateTime (int 索引，x，整数缩放 java.sql.Time 布尔 forceEncrypt)   <br/><br/> 公共 void updateTimestamp (int 索引，x，int 缩放 java.sql.Timestamp 布尔 forceEncrypt)   <br/><br/> 公共 void updateDateTime (int 索引，x，整数缩放 java.sql.Timestamp 布尔 forceEncrypt)   <br/><br/> 公共 void updateSmallDateTime (int 索引，x，整数缩放 java.sql.Timestamp 布尔 forceEncrypt)   <br/><br/>  公共 void updateDateTimeOffset (int 索引，x，整数缩放 microsoft.sql.DateTimeOffset 布尔 forceEncrypt)  <br/><br/> 公共 void updateUniqueIdentifier （int 索引，x，布尔 forceEncrypt 字符串）    <br/><br/>  公共 void updateObject （int 索引，对象 x、 int 精度、 布尔 forceEncrypt 的 int 小数位数）  <br/><br/>  公共 void updateObject （int 索引、 对象 obj、 SQLType targetSqlType、 int 缩放、 布尔 forceEncrypt）  <br/><br/> 公共 void updateBoolean （字符串 columnName、 布尔 x、 布尔 forceEncrypt）    <br/><br/>  公共 void updateByte （字符串 columnName，x，布尔 forceEncrypt 字节）  <br/><br/>  公共 void updateShort （字符串 columnName、 短 x、 布尔 forceEncrypt）  <br/><br/> 公共 void updateInt （字符串 columnName，x，布尔 forceEncrypt int）   <br/><br/>   公共 void updateLong （字符串 columnName、 长时间 x、 布尔 forceEncrypt） <br/><br/>  公共 void updateFloat （字符串 columnName、 float x、 布尔 forceEncrypt）  <br/><br/>  公共 void updateDouble （字符串 columnName、 双线 x，布尔 forceEncrypt）  <br/><br/> 公共 void updateBigDecimal (字符串 columnName，x，布尔 forceEncrypt BigDecimal)   <br/><br/>  公共 void updateBigDecimal （字符串 columnName，x，整数精度 BigDecimal，整数缩放，布尔 forceEncrypt）  <br/><br/> 公共 void updateString (字符串 columnName，x，布尔 forceEncrypt 字符串)   <br/><br/>  公共 void updateBytes （字符串 columnName、 字节 x[]、 布尔 forceEncrypt）  <br/><br/> 公共 void updateDate （字符串 columnName，x，布尔 forceEncrypt java.sql.Date）   <br/><br/>  公共 void updateTime (字符串 columnName，x，int 缩放 java.sql.Time 布尔 forceEncrypt)  <br/><br/>  公共 void updateTimestamp (字符串 columnName，x，int 缩放 java.sql.Timestamp 布尔 forceEncrypt)  <br/><br/> 公共 void updateDateTime (字符串 columnName，x，int 缩放 java.sql.Timestamp 布尔 forceEncrypt)   <br/><br/>  公共 void updateSmallDateTime (字符串 columnName，x，int 缩放 java.sql.Timestamp 布尔 forceEncrypt)  <br/><br/>  公共 void updateDateTimeOffset (字符串 columnName，x，int 缩放 microsoft.sql.DateTimeOffset 布尔 forceEncrypt)  <br/><br/>  公共 void updateUniqueIdentifier (字符串 columnName，x，布尔 forceEncrypt 字符串)<br/><br/>公共 void updateObject （字符串 columnName，对象 x、 int 精度、 布尔 forceEncrypt 的 int 小数位数）<br/><br/>公共 void updateObject （字符串 columnName、 对象 obj、 SQLType targetSqlType、 int 缩放、 布尔 forceEncrypt）|为给定的 java 值更新指定的列。<br/><br/>如果布尔 forceEncrypt 设置为 true，将列将仅设置如果对其进行加密，并且针对连接还是的语句上启用始终加密。<br/><br/>如果布尔 forceEncrypt 设置为 false，该驱动程序不会强制对参数加密。|

  
中的新类型**microsoft.sql.Types**类
|Name|Description|  
|----------|-----------------|  
|DATETIME、 SMALLDATETIME、 MONEY、 SMALLMONEY、 GUID|发送到的参数值时为目标 SQL 类型使用这些类型**加密**datetime、 smalldatetime、 money、 smallmoney、 uniqueidentifier 列使用 setObject()/updateObject() API 方法。|  
  
  
 **SQLServerStatementColumnEncryptionSetting 枚举**  
  
 指定将如何发送和接收时读取和写入加密的列数据。 根据特定的查询，对性能的影响可能会降低通过跳过 Always Encrypted 驱动程序的处理时正在使用非加密列。 请注意，这些设置不能用于绕过加密以及获取纯文本数据的访问权限。  
  
 **语法**  
  
```  
Public enum  SQLServerStatementColumnEncryptionSetting  
```  
  
 **成员**  
  
|Name|Description|  
|----------|-----------------|  
|UseConnectionSetting|指定该命令应默认为连接字符串中的始终加密设置。|  
|已启用|查询中启用始终加密。|  
|ResultSetOnly|指定驱动程序中 Always Encrypted 例程应处理该命令的结果。 当该命令不具有需要加密的任何参数，请使用此值。|  
|禁用|查询中禁用始终加密。|  
  
 要从中的语句级别设置添加到 SQLServerConnection 类 SQLServerConnectionPoolProxy 类。 这些类中的以下方法是使用新的设置超负荷。  
  
|Name|Description|  
|----------|-----------------|  
|公共语句 createStatement （int nType、 int nConcur、 int statementHoldability、 SQLServerStatementColumnEncryptionSetting stmtColEncSetting）|创建一个将生成使用给定的类型、 并发、 保持能力和列的加密设置的结果集对象的语句对象。|  
|公共 CallableStatement prepareCall （字符串 sql、 int nType、 int nConcur、 int statementHoldability、 SQLServerStatementColumnEncryptionSetting stmtColEncSetiing）|使用将生成具有给定的类型、 并发和保持能力的结果集对象的给定的列加密设置创建 CallableStatement 对象。|  
|公共 PreparedStatement prepareStatement （字符串 sql、 int autogeneratedKeys、 SQLServerStatementColumnEncryptionSetting stmtColEncSetting）|使用能够检索自动生成的密钥的给定的列加密设置创建 PreparedStatement 对象。|  
|公共 PreparedStatement prepareStatement （字符串 sql、 字符串 [] columnNames、 SQLServerStatementColumnEncryptionSetting stmtColEncSetting）|使用将生成具有给定的列名的结果集对象的给定的列加密设置创建 PreparedStatement 对象。|  
|公共 PreparedStatement prepareStatement （字符串 sql、 int [] columnIndexes、 SQLServerStatementColumnEncryptionSetting stmtColEncSetting|使用将生成与给定的列索引的结果集对象的给定的列加密设置创建 PreparedStatement 对象。|  
|公共 PreparedStatement prepareStatement （字符串 sql、 int nType、 int nConcur、 int nHold、 SQLServerStatementColumnEncryptionSetting stmtColEncSetting）|使用将生成具有给定的类型、 并发和保持能力的结果集对象的给定的列加密设置创建 PreparedStatement 对象。|  
  
> [!NOTE]  
>  如果查询禁用了始终加密，并且查询具有需要加密 （参数对应于加密列） 的参数，则查询将失败。  
>   
>  如果查询禁用了始终加密，并且查询从加密列中返回结果，查询将返回加密的值。 加密的值将具有 varbinary 数据类型。  
  
## <a name="see-also"></a>另请参阅  
 [对 JDBC 驱动程序使用始终加密](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
  
  

