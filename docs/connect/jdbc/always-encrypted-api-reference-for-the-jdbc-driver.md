---
title: "始终加密的 JDBC 驱动程序的 API 参考 |Microsoft 文档"
ms.custom: 
ms.date: 1/19/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6962a2aa-9508-4d4f-a78c-905e2bc68615
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e3ed6ba1720ffff58967b4deaeda04194dcf156a
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2018
---
# <a name="always-encrypted-api-reference-for-the-jdbc-driver"></a>始终加密的 JDBC 驱动程序的 API 参考
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  始终加密允许客户端对客户端应用程序内的敏感数据进行加密，并且永远不向 SQL Server 显示加密密钥。 安装在客户端计算机上的启用始终加密的驱动程序通过在 SQL Server 客户端应用程序中对敏感数据进行加密和解密来实现此目标。 该驱动程序先对敏感列中的数据进行加密，然后再将该数据传递到 SQL Server，并且自动重写查询以便保留应用程序的语义。 同样，该驱动程序以透明方式对存储在加密数据库列（包含在查询结果中）中的数据进行解密。 有关详细信息，请参阅[始终加密 （数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)和[Using Always Encrypted with JDBC 驱动程序](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  始终加密功能支持的 Microsoft JDBC Driver 6.0 或更高版本的 SQL Server 2016 的 SQL Server。  
  
 ## <a name="always-encrypted-api-references"></a>始终加密 API 参考
 
 对 JDBC 驱动程序 API 有多次新的添加和修改，以供在使用始终加密的客户端应用程序中使用。  
  
 **SQLServerConnection 类**  
  
|名称|Description|  
|----------|-----------------|  
|新的连接字符串关键字：<br /><br /> columnEncryptionSetting|columnEncryptionSetting = 已启用启用始终加密功能的连接和 columnEncryptionSetting = 已禁用禁用它。 接受的值为“启用”/“禁用”。 默认值为“禁用”。|  
|新方法：<br /><br /> 公共静态 void setColumnEncryptionTrustedMasterKeyPaths (映射 < 字符串，则列表\<字符串 >> trustedKeyPaths)<br /><br /> 公共静态 void updateColumnEncryptionTrustedMasterKeyPaths (字符串服务器，列表\<字符串 > trustedKeyPaths)<br /><br /> public static void removeColumnEncryptionTrustedMasterKeyPaths(String server)|允许你为集/更新/删除的受信任密钥路径列表的数据库服务器。 如果在处理应用程序查询时，驱动程序收到不在列表上的密钥路径，则查询将失败。 此属性提供针对安全攻击的额外保护，这些攻击涉及到提供伪造密钥路径的受损 SQL Server，这可能导致泄露密钥存储凭据。|  
|新方法：<br /><br /> public static Map<String, List\<String>> getColumnEncryptionTrustedMasterKeyPaths()|为数据库服务器返回受信任的密钥路径的列表。|  
|新方法：<br /><br /> 公共静态 void registerColumnEncryptionKeyStoreProviders (映射\<字符串、 SQLServerColumnEncryptionKeyStoreProvider > clientKeyStoreProviders)|允许你注册自定义密钥存储提供程序。 它是一个将密钥存储提供程序名称映射到密钥存储提供程序实现的字典。<br /><br /> 若要使用 JVM 密钥存储，你需要使用 JVM 密钥存储凭据实例化 SQLServerColumnEncryptionJVMKeyStoreProvider 对象，并向驱动程序注册它。 为此提供程序名称必须是 MSSQL_JVM_KEYSTORE。<br /><br /> 若要使用 Azure 密钥保管库存储你需要实例化 SQLServerColumnEncryptionAzureKeyStoreProvider 对象并将它注册到该驱动程序。 为此提供程序名称必须是 AZURE_KEY_VAULT。|
|公共最终布尔 getSendTimeAsDatetime()|返回 sendTimeAsDatetime 连接属性的设置。|
|公共 void setSendTimeAsDatetime (布尔 sendTimeAsDateTimeValue)|修改 sendTimeAsDatetime 连接属性的设置。|

 **SQLServerConnectionPoolProxy 类**
|名称|Description|  
|----------|-----------------|  
|公共最终布尔 getSendTimeAsDatetime()|返回 sendTimeAsDatetime 连接属性的设置。|
|公共 void setSendTimeAsDatetime (布尔 sendTimeAsDateTimeValue)|修改 sendTimeAsDatetime 连接属性的设置。|
     
  
 **SQLServerDataSource 类**  
  
|名称|Description|  
|----------|-----------------|  
|public void setColumnEncryptionSetting(String columnEncryptionSetting)|为数据源对象启用/禁用始终加密功能。<br /><br /> 默认值为“禁用”。|  
|public String getColumnEncryptionSetting()|检索数据源对象的始终加密功能设置。|
|公共 void setKeyStoreAuthentication (字符串 keyStoreAuthentication)|设置标识的密钥存储的名称。 支持的值是识别 Java 密钥存储"JavaKeyStorePassword"。<br/><br/>默认值为 null。|
|public String getKeyStoreAuthentication()|获取数据源对象的 keyStoreAuthentication 设置的值。|
|公共 void setKeyStoreSecret (字符串 keyStoreSecret)|设置 Java 密钥库的密码。 请注意，Java 密钥存储提供程序密钥库和密钥的密码必须相同。 请注意，必须使用"JavaKeyStorePassword"设置 keyStoreAuthentication。|
|公共 void setKeyStoreLocation (字符串 keyStoreLocation)|设置包括 Java 密钥库的文件名称的位置。 请注意，必须使用"JavaKeyStorePassword"设置 keyStoreAuthentication。|
|public String getKeyStoreLocation()|检索有关 Java 密钥存储 keyStoreLocation。|
  
 **SQLServerColumnEncryptionJavaKeyStoreProvider 类**  
  
 Java 密钥存储的密钥存储提供程序实现。 此类允许使用 Java 密钥库中存储为列主密钥的证书。  
  
 构造函数  
  
|名称|Description|  
|----------|-----------------|  
|public SQLServerColumnEncryptionJavaKeyStoreProvider (String keyStoreLocation, char[] keyStoreSecret)|用于 Java 密钥存储的密钥存储提供程序。|  
  
 方法  
  
|名称|Description|  
|----------|-----------------|  
|公共字节 [] decryptColumnEncryptionKey （字符串 masterKeyPath、 字符串 encryptionAlgorithm、 字节 [] encryptedColumnEncryptionKey）|解密列加密密钥的指定加密值。 预期使用带有指定密钥路径的证书并使用指定算法加密该加密值。<br /><br /> **密钥路径的格式应为以下项之一：**<br /><br /> 指纹：<certificate_thumbprint><br /><br /> 别名：<certificate_alias><br /><br /> （重写 SQLServerColumnEncryptionKeyStoreProvider。 decryptColumnEncryptionKey(String, String, Byte[]).)|  
|公共字节 [] encryptColumnEncryptionKey （字符串 masterKeyPath、 字符串 encryptionAlgorithm、 字节 [] plainTextColumnEncryptionKey）|使用带有指定密钥路径的证书并使用指定算法加密列加密密钥。<br /><br /> **密钥路径的格式应为以下项之一：**<br /><br /> 指纹：<certificate_thumbprint><br /><br /> 别名：<certificate_alias><br /><br /> （重写 SQLServerColumnEncryptionKeyStoreProvider。 encryptColumnEncryptionKey(String, String, Byte[]).)|  
|公共 void setName （字符串名称）|设置此密钥存储提供程序的名称。|
|公共字符串 getName （)|获取此密钥存储提供程序的名称。|
  
 **SQLServerColumnEncryptionAzureKeyVaultProvider 类**  
  
 Azure 密钥保管库的密钥存储提供程序实现。 此类，可使用 Azure 密钥保管库中存储为列主密钥的密钥。  
  
 构造函数  
  
|名称|Description|  
|----------|-----------------|  
|公共 SQLServerColumnEncryptionAzureKeyVaultProvider （字符串 clientId，字符串 clientKey）|Azure 密钥保管库的密钥存储提供程序。  你需要提供标识符和客户端请求令牌向 Azure 密钥保管库进行身份验证密钥。|  
  
 方法  
  
|名称|Description|  
|----------|-----------------|  
|公共字节 [] decryptColumnEncryptionKey （字符串 masterKeyPath、 字符串 encryptionAlgorithm、 字节 [] encryptedColumnEncryptionKey）|解密列加密密钥的指定加密值。 加密的值预期应使用和进行加密指定的列键 IDmaster 键使用指定的算法。 <br />（重写 SQLServerColumnEncryptionKeyStoreProvider。 decryptColumnEncryptionKey(String, String, Byte[]).)|  
|公共字节 [] encryptColumnEncryptionKey （字符串 masterKeyPath、 字符串 encryptionAlgorithm、 字节 [] columnEncryptionKey）|对列加密密钥使用指定的列主密钥和使用指定的算法进行加密。 <br />（重写 SQLServerColumnEncryptionKeyStoreProvider。 encryptColumnEncryptionKey(String, String, Byte[]).)|  
|公共 void setName （字符串名称）|设置此密钥存储提供程序的名称。|
|公共字符串 getName （)|获取此密钥存储提供程序的名称。|  
  
  
 **SQLServerKeyVaultAuthenticationCallback Interface**  
  
 此接口包含用于 Azure 密钥保管库身份验证，这是由用户来实现的一个方法。  
  
 方法  
  
|名称|Description|  
|----------|-----------------|  
|公共字符串 getAccessToken （字符串机构、 字符串资源、 String scope）;|该方法所需中重写。 方法用于获取访问令牌向 Azure 密钥保管库。|  
  
 **SQLServerColumnEncryptionKeyStoreProvider 类**  
  
 扩展此类以实现自定义密钥存储提供程序。  
  
|名称|Description|  
|----------|-----------------|  
|SQLServerColumnEncryptionKeyStoreProvider|所有密钥存储提供程序的基类。 自定义提供程序必须从此类派生和重写其成员函数，然后注册它使用 SQLServerConnection。 registerColumnEncryptionKeyStoreProviders().|  
  
 方法  
  
|名称|Description|  
|----------|-----------------|  
|public abstract byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)|用于解密列加密密钥的指定加密值的基类方法。 预期使用带有指定密钥路径的列主密钥并使用指定算法加密该加密值。|  
|public abstract byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[]  columnEncryptionKey)|用于使用带有指定密钥路径的列主密钥并使用指定算法加密列加密密钥的基类算法。|
|公共抽象 void setName （字符串名称）|设置此密钥存储提供程序的名称。|
|公共抽象字符串 getName()|获取此密钥存储提供程序的名称。|  
  
 中的新的或重载方法**SQLServerPreparedStatement**类  
  
|名称|Description|  
|----------|-----------------|  
|公共 void setBigDecimal (int parameterIndex，x，int 精度 BigDecimal int 缩放)<br /><br /> public void setObject(int parameterIndex, Object x, int targetSqlType, Integer precision, int scale)<br /><br /> public void setObject(int parameterIndex, Object x, SQLType targetSqlType, Integer precision, Integer scale)<br /><br /> public void setTime(int parameterIndex, java.sql.Time x, int scale)<br /><br /> public void setTimestamp(int parameterIndex, java.sql.Timestamp x, int scale) <br />public void setDateTimeOffset(int parameterIndex, microsoft.sql.DateTimeOffset x, int scale)|这些方法将重载与精度或小数位数参数和 / 或以特定的数据类型，需要精度和小数位数信息支持始终加密。|  
|公共 void setMoney (int parameterIndex，BigDecimal x)<br /><br /> 公共 void setSmallMoney (int parameterIndex，BigDecimal x)<br /><br /> 公共 void setUniqueIdentifier （int parameterIndex，字符串 guid）<br /><br /> public void setDateTime(int parameterIndex, java.sql.Timestamp x)<br /><br /> public void setSmallDateTime(int parameterIndex, java.sql.Timestamp x)|这些方法将添加以支持始终加密的数据类型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime。 <br/><br/>请注意，用于将参数值发送到加密的 datetime2 列使用现有的 setTimestamp() 方法。 用于加密的日期时间和 smalldatetime 列的新方法 setDateTime() 和 setSmallDateTime() 分别使用。|  
|公共最终 void setBigDecimal （int parameterIndex，x，int 精度 BigDecimal，int 缩放，布尔 forceEncrypt）<br /><br /> 公共最终 void setMoney (int parameterIndex，x，布尔 forceEncrypt BigDecimal)<br /><br /> 公共最终 void setSmallMoney (int parameterIndex，x，布尔 forceEncrypt BigDecimal)<br /><br /> 公共最终 void setBoolean （int parameterIndex、 布尔 x、 布尔 forceEncrypt）<br /><br /> 公共最终 void setByte （int parameterIndex，x，布尔 forceEncrypt 字节）<br /><br /> 公共最终 void setBytes （int parameterIndex、 字节 x[]、 布尔 forceEncrypt）<br /><br /> 公共最终 void setUniqueIdentifier （int parameterIndex、 字符串 guid、 布尔 forceEncrypt）<br /><br /> 公共最终 void setDouble （int parameterIndex、 双线 x，布尔 forceEncrypt）<br /><br /> 公共最终 void setFloat （int parameterIndex、 float x、 布尔 forceEncrypt）<br /><br /> 公共最终 void setInt （int parameterIndex、 int 值、 布尔 forceEncrypt）<br /><br /> 公共最终 void setLong （int parameterIndex、 长时间 x、 布尔 forceEncrypt）<br /><br /> public final setObject(int parameterIndex, Object x, int targetSqlType, Integer precision, int scale, boolean forceEncrypt)<br /><br /> public final void setObject(int parameterIndex, Object x, SQLType targetSqlType, Integer precision, Integer scale, boolean forceEncrypt)<br /><br /> 公共最终 void setShort （int parameterIndex、 短 x、 布尔 forceEncrypt）<br /><br /> 公共最终 void setString (int parameterIndex，字符串 str 布尔 forceEncrypt)<br /><br /> 公共最终 void setNString （int parameterIndex、 字符串值、 布尔 forceEncrypt）<br /><br /> public final void setTime(int parameterIndex, java.sql.Time x, int scale, boolean forceEncrypt)<br /><br /> public final void setTimestamp(int parameterIndex, java.sql.Timestamp x, int scale, boolean forceEncrypt)<br /><br /> public final void setDateTimeOffset(int parameterIndex, microsoft.sql.DateTimeOffset x, int scale, boolean forceEncrypt)<br /><br /> public final void setDateTime(int parameterIndex, java.sql.Timestamp x, boolean forceEncrypt)<br /><br /> public final void setSmallDateTime(int parameterIndex, java.sql.Timestamp x, boolean forceEncrypt)<br /><br /> public final void setDate(int parameterIndex, java.sql.Date x, java.util.Calendar cal, boolean forceEncrypt)<br /><br /> public final void setTime(int parameterIndex, java.sql.Time x, java.util.Calendar cal, boolean forceEncrypt)<br /><br /> public final void setTimestamp(int parameterIndex, java.sql.Timestamp x, java.util.Calendar cal, boolean forceEncrypt)|将指定的参数设置为给定的 java 值。<br /><br /> 如果布尔 forceEncrypt 设置为 true，查询将仅当将参数设置标识列加密，对连接或语句上启用始终加密。<br /><br /> 如果布尔 forceEncrypt 设置为 false，该驱动程序不会强制对参数加密。|  
  
 中的新的或重载方法**SQLServerCallableStatement**类  
  
|名称|Description|  
|----------|-----------------|  
|public void registerOutParameter(int parameterIndex, int sqlType, int precision, int scale)<br /><br /> 公共 void registerOutParameter （int parameterIndex、 SQLType sqlType、 int 精度、 int 缩放）<br /><br /> 公共 void registerOutParameter （字符串 parameterName、 int sqlType、 int 精度、 int 缩放）<br /><br /> 公共 void registerOutParameter （字符串 parameterName、 SQLType sqlType、 int 精度、 int 缩放）<br />公共 void setBigDecimal （字符串 parameterName、 BigDecimal bd，int 精度、 int 缩放）<br /><br /> public void setTime(String parameterName, java.sql.Time t, int scale)<br /><br /> public void setTimestamp(String parameterName, java.sql.Timestamp t, int scale)<br /><br /> public void setDateTimeOffset(String parameterName, microsoft.sql.DateTimeOffset t, int scale)<br/><br/>公共最终 void setObject （字符串 sCol，对象 x、 int targetSqlType、 整数精度，int 小数位数）|这些方法将重载与精度或小数位数参数和 / 或以特定的数据类型，需要精度和小数位数信息支持始终加密。|  
|public void setDateTime(String parameterName, java.sql.Timestamp x)<br /><br /> public void setSmallDateTime(String parameterName, java.sql.Timestamp x)<br /><br /> 公共 void setUniqueIdentifier （字符串参数名称，字符串 guid）<br /><br /> 公共 void setMoney （字符串 parameterName，BigDecimal bd）<br /><br /> 公共 void setSmallMoney （字符串 parameterName，BigDecimal bd）<br/><br/>公共时间戳 getDateTime （int 索引）<br/><br/>公共时间戳 getDateTime (字符串 sCol)<br/><br/>公共时间戳 getDateTime （int 索引，日历 cal）<br/><br/>public Timestamp getSmallDateTime(int index)<br/><br/>公共时间戳 getSmallDateTime (字符串 sCol)<br/><br/>公共时间戳 getSmallDateTime （int 索引，日历 cal）<br/><br/>公共时间戳 getSmallDateTime （字符串名称，日历 cal）<br/><br/>公共 BigDecimal getMoney （int 索引）<br/><br/>公共 BigDecimal getMoney (字符串 sCol)<br/><br/>公共 BigDecimal getSmallMoney （int 索引）<br/><br/>公共 BigDecimal getSmallMoney (字符串 sCol)|这些方法将添加以支持始终加密的数据类型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime。 <br/><br/>请注意，用于将参数值发送到加密的 datetime2 列使用现有的 setTimestamp() 方法。 用于加密的日期时间和 smalldatetime 列的新方法 setDateTime() 和 setSmallDateTime() 分别使用。|  
|公共 void setObject （字符串参数名称、 Object o、 int n、 int m、 布尔 forceEncrypt）<br /><br /> 公共 void setObject （字符串参数名称、 对象 obj、 SQLType jdbcType、 int 缩放、 布尔 forceEncrypt）<br /><br /> public void setDate(String parameterName, java.sql.Date x, Calendar c, boolean forceEncrypt)<br /><br /> public void setTime(String parameterName, java.sql.Time t, int scale, boolean forceEncrypt)<br /><br /> public void setTime(String parameterName, java.sql.Time x, Calendar c, boolean forceEncrypt)<br /><br /> public void setDateTime(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)<br /><br /> public void setDateTimeOffset(String parameterName, microsoft.sql.DateTimeOffset t, int scale, boolean forceEncrypt)<br /><br /> public void setSmallDateTime(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)<br /><br /> public void setTimestamp(String parameterName, java.sql.Timestamp t, int scale, boolean forceEncrypt)<br /><br /> public void setTimestamp(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)<br /><br /> 公共 void setUniqueIdentifier （字符串参数名称、 guid 字符串、 布尔 forceEncrypt）<br /><br /> 公共 void setBytes （字符串 parameterName、 字节 [] b、 布尔 forceEncrypt）<br /><br /> 公共 void setByte （字符串 parameterName、 字节 b、 布尔 forceEncrypt）<br /><br /> 公共 void setString （字符串 parameterName、 字符串 s、 布尔 forceEncrypt）<br /><br /> （字符串 parameterName、 字符串值、 布尔 forceEncrypt） 的公共最终 void setNString<br /><br /> 公共 void setMoney （字符串 parameterName、 BigDecimal bd，布尔 forceEncrypt）<br /><br /> 公共 void setSmallMoney （字符串 parameterName、 BigDecimal bd，布尔 forceEncrypt）<br /><br /> 公共 void setBigDecimal （字符串 parameterName、 BigDecimal bd，int 精度、 int 缩放、 布尔 forceEncrypt）<br /><br /> 公共 void setDouble （字符串 parameterName、 双线 d，布尔 forceEncrypt）<br /><br /> 公共 void setFloat （字符串 parameterName、 float f、 布尔 forceEncrypt）<br /><br /> 公共 void setInt (字符串 parameterName、 int i，布尔 forceEncrypt)<br /><br /> 公共 void setLong （字符串 parameterName、 长时间 l、 布尔 forceEncrypt）<br /><br /> 公共 void setShort （字符串 parameterName、 短 s 整数、 布尔 forceEncrypt）<br /><br /> 公共 void setBoolean （字符串 parameterNames、 布尔值 b、 布尔 forceEncrypt）<br/><br/>public void setTimeStamp(String sCol, java.sql.Timestamp x, Calendar c, Boolean forceEncrypt)|将指定的参数设置为给定的 java 值。<br /><br /> 如果布尔 forceEncrypt 设置为 true，查询将仅当将参数设置标识列加密，对连接或语句上启用始终加密。<br /><br /> 如果布尔 forceEncrypt 设置为 false，该驱动程序不会强制对参数加密。|
 

 中的新的或重载方法**SQLServerResultSet**类  
  
|名称|Description|  
|----------|-----------------|  
|公共字符串 getUniqueIdentifier (int columnIndex)<br/><br/>公共字符串 getUniqueIdentifier (字符串 columnLabel)<br/><br/>   public java.sql.Timestamp getDateTime(int columnIndex) <br/><br/> public java.sql.Timestamp getDateTime(String columnName)   <br/><br/> public java.sql.Timestamp getDateTime(int columnIndex, Calendar cal)   <br/><br/>public java.sql.Timestamp getDateTime(String colName, Calendar cal)    <br/><br/>public java.sql.Timestamp getSmallDateTime(int columnIndex)    <br/><br/> public java.sql.Timestamp getSmallDateTime(String columnName)   <br/><br/> public java.sql.Timestamp getSmallDateTime(int columnIndex, Calendar cal)   <br/><br/> public java.sql.Timestamp getSmallDateTime(String colName, Calendar cal)   <br/><br/>  公共 BigDecimal getMoney (int columnIndex)  <br/><br/> 公共 BigDecimal getMoney (字符串 columnName)   <br/><br/> 公共 BigDecimal getSmallMoney (int columnIndex)   <br/><br/>  公共 BigDecimal getSmallMoney (字符串 columnName)  <br/><br/>public void updateMoney(String columnName, BigDecimal x)    <br/><br/>  public void updateSmallMoney(String columnName, BigDecimal x)  <br/><br/>     public void updateDateTime(int index, java.sql.Timestamp x) <br/><br/> public void updateSmallDateTime(int index, java.sql.Timestamp x) |这些方法将添加以支持始终加密的数据类型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime。 <br/><br/>请注意，用于更新加密的 datetime2 列使用现有的 updateTimestamp() 方法。 用于加密的日期时间和 smalldatetime 列的新方法 updateDateTime() 和 updateSmallDateTime() 分别使用。|
|公共 void updateBoolean （int 索引、 布尔 x、 布尔 forceEncrypt）  <br/><br/>  公共 void updateByte （int 索引，x，布尔 forceEncrypt 字节）  <br/><br/>  公共 void updateShort （int 索引、 短 x、 布尔 forceEncrypt）  <br/><br/> 公共 void updateInt （int 索引，x，布尔 forceEncrypt int）   <br/><br/>  公共 void updateLong （int 索引、 长时间 x、 布尔 forceEncrypt）  <br/><br/> 公共 void updateFloat （int 索引、 float x、 布尔 forceEncrypt）   <br/><br/> 公共 void updateDouble （int 索引、 双线 x，布尔 forceEncrypt）   <br/><br/> 公共 void updateMoney （int 索引，x，布尔 forceEncrypt BigDecimal）   <br/><br/>  公共 void updateMoney (字符串 columnName，x，布尔 forceEncrypt BigDecimal)  <br/><br/> 公共 void updateSmallMoney （int 索引，x，布尔 forceEncrypt BigDecimal）   <br/><br/>  public void updateSmallMoney(String columnName, BigDecimal x, boolean forceEncrypt)  <br/><br/> public void updateBigDecimal(int index, BigDecimal x, Integer precision, Integer scale, boolean forceEncrypt)   <br/><br/>  公共 void updateString （int columnIndex、 字符串 stringValue、 布尔 forceEncrypt）  <br/><br/>  公共 void updateNString （int columnIndex、 字符串 nString、 布尔 forceEncrypt）  <br/><br/>  公共 void updateNString （字符串 columnLabel、 字符串 nString、 布尔 forceEncrypt）  <br/><br/> 公共 void updateBytes （int 索引、 字节 x[]、 布尔 forceEncrypt）   <br/><br/>  public void updateDate(int index, java.sql.Date x, boolean forceEncrypt)  <br/><br/> public void updateTime(int index, java.sql.Time x, Integer scale, boolean forceEncrypt)   <br/><br/> public void updateTimestamp(int index, java.sql.Timestamp x, int scale, boolean forceEncrypt)   <br/><br/> public void updateDateTime(int index, java.sql.Timestamp x, Integer scale, boolean forceEncrypt)   <br/><br/> public void updateSmallDateTime(int index, java.sql.Timestamp x, Integer scale, boolean forceEncrypt)   <br/><br/>  public void updateDateTimeOffset(int index, microsoft.sql.DateTimeOffset x, Integer scale, boolean forceEncrypt)  <br/><br/> 公共 void updateUniqueIdentifier （int 索引，x，布尔 forceEncrypt 字符串）    <br/><br/>  公共 void updateObject （int 索引，对象 x、 int 精度、 布尔 forceEncrypt 的 int 小数位数）  <br/><br/>  public void updateObject(int index, Object obj, SQLType targetSqlType, int scale, boolean forceEncrypt)  <br/><br/> 公共 void updateBoolean （字符串 columnName、 布尔 x、 布尔 forceEncrypt）    <br/><br/>  公共 void updateByte （字符串 columnName，x，布尔 forceEncrypt 字节）  <br/><br/>  公共 void updateShort （字符串 columnName、 短 x、 布尔 forceEncrypt）  <br/><br/> 公共 void updateInt （字符串 columnName，x，布尔 forceEncrypt int）   <br/><br/>   公共 void updateLong （字符串 columnName、 长时间 x、 布尔 forceEncrypt） <br/><br/>  公共 void updateFloat （字符串 columnName、 float x、 布尔 forceEncrypt）  <br/><br/>  公共 void updateDouble （字符串 columnName、 双线 x，布尔 forceEncrypt）  <br/><br/> public void updateBigDecimal(String columnName, BigDecimal x, boolean forceEncrypt)   <br/><br/>  public void updateBigDecimal(String columnName, BigDecimal x, Integer precision, Integer scale, boolean forceEncrypt)  <br/><br/> 公共 void updateString (字符串 columnName，x，布尔 forceEncrypt 字符串)   <br/><br/>  public void updateBytes(String columnName, byte x[], boolean forceEncrypt)  <br/><br/> public void updateDate(String columnName, java.sql.Date x, boolean forceEncrypt)   <br/><br/>  public void updateTime(String columnName, java.sql.Time x, int scale, boolean forceEncrypt)  <br/><br/>  public void updateTimestamp(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)  <br/><br/> public void updateDateTime(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)   <br/><br/>  public void updateSmallDateTime(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)  <br/><br/>  public void updateDateTimeOffset(String columnName, microsoft.sql.DateTimeOffset x, int scale, boolean forceEncrypt)  <br/><br/>  公共 void updateUniqueIdentifier (字符串 columnName，x，布尔 forceEncrypt 字符串)<br/><br/>公共 void updateObject （字符串 columnName，对象 x、 int 精度、 布尔 forceEncrypt 的 int 小数位数）<br/><br/>public void updateObject(String columnName, Object obj, SQLType targetSqlType, int scale, boolean forceEncrypt)|为给定的 java 值更新指定的列。<br/><br/>如果布尔 forceEncrypt 设置为 true，将列将仅设置如果对其进行加密，并且针对连接还是的语句上启用始终加密。<br/><br/>如果布尔 forceEncrypt 设置为 false，该驱动程序不会强制对参数加密。|

  
中的新类型**microsoft.sql.Types**类
|名称|Description|  
|----------|-----------------|  
|DATETIME、 SMALLDATETIME、 MONEY、 SMALLMONEY、 GUID|发送到的参数值时为目标 SQL 类型使用这些类型**加密**datetime、 smalldatetime、 money、 smallmoney、 uniqueidentifier 列使用 setObject()/updateObject() API 方法。|  
  
  
 **SQLServerStatementColumnEncryptionSetting Enum**  
  
 指定将如何发送和接收时读取和写入加密的列数据。 根据特定的查询，对性能的影响可能会降低通过跳过 Always Encrypted 驱动程序的处理时正在使用非加密列。 请注意，这些设置不能用于绕过加密以及获取纯文本数据的访问权限。  
  
 **语法**  
  
```  
Public enum  SQLServerStatementColumnEncryptionSetting  
```  
  
 **成员**  
  
|名称|Description|  
|----------|-----------------|  
|UseConnectionSetting|指定该命令应默认为连接字符串中的始终加密设置。|  
|已启用|查询中启用始终加密。|  
|ResultSetOnly|指定驱动程序中 Always Encrypted 例程应处理该命令的结果。 当该命令不具有需要加密的任何参数，请使用此值。|  
|Disabled|查询中禁用始终加密。|  
  
 要从中的语句级别设置添加到 SQLServerConnection 类 SQLServerConnectionPoolProxy 类。 这些类中的以下方法是使用新的设置超负荷。  
  
|名称|Description|  
|----------|-----------------|  
|公共语句 createStatement （int nType、 int nConcur、 int statementHoldability、 SQLServerStatementColumnEncryptionSetting stmtColEncSetting）|创建一个将生成使用给定的类型、 并发、 保持能力和列的加密设置的结果集对象的语句对象。|  
|public CallableStatement prepareCall(String sql, int nType, int nConcur, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetiing)|使用将生成具有给定的类型、 并发和保持能力的结果集对象的给定的列加密设置创建 CallableStatement 对象。|  
|public PreparedStatement prepareStatement(String sql, int autogeneratedKeys, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|使用能够检索自动生成的密钥的给定的列加密设置创建 PreparedStatement 对象。|  
|public PreparedStatement prepareStatement(String sql, String[] columnNames, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|使用将生成具有给定的列名的结果集对象的给定的列加密设置创建 PreparedStatement 对象。|  
|public PreparedStatement prepareStatement(String sql, int[] columnIndexes, SQLServerStatementColumnEncryptionSetting stmtColEncSetting|使用将生成与给定的列索引的结果集对象的给定的列加密设置创建 PreparedStatement 对象。|  
|public PreparedStatement prepareStatement( String sql, int nType, int nConcur, int nHold, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|使用将生成具有给定的类型、 并发和保持能力的结果集对象的给定的列加密设置创建 PreparedStatement 对象。|  
  
> [!NOTE]  
>  如果查询禁用了始终加密，并且查询具有需要加密 （参数对应于加密列） 的参数，则查询将失败。  
>   
>  如果查询禁用了始终加密，并且查询从加密列中返回结果，查询将返回加密的值。 加密的值将具有 varbinary 数据类型。  
  
 ## <a name="see-also"></a>另请参阅  
 [对 JDBC 驱动程序使用始终加密](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
  

