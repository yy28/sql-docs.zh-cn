---
title: JDBC 驱动程序的 Always Encrypted API 参考 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6962a2aa-9508-4d4f-a78c-905e2bc68615
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1b720a607b702e93643d70b40a5e6ab036f2f56
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2018
ms.locfileid: "39279248"
---
# <a name="always-encrypted-api-reference-for-the-jdbc-driver"></a>JDBC 驱动程序的 Always Encrypted API 参考
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  始终加密允许客户端对客户端应用程序内的敏感数据进行加密，并且永远不向 SQL Server 显示加密密钥。 安装在客户端计算机上的启用 Always Encrypted 的驱动程序通过在 SQL Server 客户端应用程序中对敏感数据进行加密和解密来实现此功能。 该驱动程序先对敏感列中的数据进行加密，然后再将该数据传递到 SQL Server，并且自动重写查询以便保留应用程序的语义。 同样，该驱动程序以透明方式对存储在加密数据库列（在查询结果中）中的数据进行解密。 有关详细信息，请参阅[Always Encrypted （数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)并[JDBC 驱动程序中使用 Always Encrypted](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  在 SQL Server 2016 中，Always Encrypted 仅受 Microsoft JDBC Driver 6.0 for SQL Server 和更高版本支持。  
  
 ## <a name="always-encrypted-api-references"></a>Always Encrypted API 参考
 
 对 JDBC 驱动程序 API 有多次新的添加和修改，以供在使用始终加密的客户端应用程序中使用。  
  
 **SQLServerConnection 类**  
  
|“属性”|描述|  
|----------|-----------------|  
|新的连接字符串关键字：<br /><br /> columnEncryptionSetting|columnEncryptionSetting=Enabled 为该连接启用 Always Encrypted 功能，而 columnEncryptionSetting=Disabled 禁用该功能。 接受的值为“启用”/“禁用”。 默认值为“禁用”。|  
|新方法：<br /><br /> 公共静态 void setColumnEncryptionTrustedMasterKeyPaths (映射 < 字符串，列出\<字符串 >> trustedKeyPaths)<br /><br /> 公共静态 void updateColumnEncryptionTrustedMasterKeyPaths (字符串服务器，列表\<字符串 > trustedKeyPaths)<br /><br /> 公共静态 void removeColumnEncryptionTrustedMasterKeyPaths (字符串 server)|允许为数据库服务器设置/更新/删除受信任的密钥路径的列表。 如果在处理应用程序查询时，驱动程序收到不在列表上的密钥路径，则查询将失败。 此属性提供针对安全攻击的额外保护，这些攻击涉及到发送伪造密钥路径的受损 SQL Server，这可能导致泄露密钥存储凭据。|  
|新方法：<br /><br /> public static Map<String, List\<String>> getColumnEncryptionTrustedMasterKeyPaths()|为数据库服务器返回受信任的密钥路径的列表。|  
|新方法：<br /><br /> public static void registerColumnEncryptionKeyStoreProviders (Map\<String, SQLServerColumnEncryptionKeyStoreProvider> clientKeyStoreProviders)|允许你注册自定义密钥存储提供程序。 它是一个将密钥存储提供程序名称映射到密钥存储提供程序实现的字典。<br /><br /> 若要使用 JVM 密钥存储，需要使用 JVM 密钥存储凭据实例化 SQLServerColumnEncryptionJVMKeyStoreProvider 对象，并使用驱动程序注册它。 此提供程序的名称必须为“MSSQL_JVM_KEYSTORE”。<br /><br /> 若要使用 Azure 密钥保管库存储区，需要实例化 SQLServerColumnEncryptionAzureKeyStoreProvider 对象并将其注册的驱动程序。 为此提供程序名称必须是 AZURE_KEY_VAULT。|
|public final boolean getSendTimeAsDatetime()|返回 sendTimeAsDatetime 连接属性的设置。|
|public void setSendTimeAsDatetime (布尔 sendTimeAsDateTimeValue)|修改 sendTimeAsDatetime 连接属性的设置。|

 **SQLServerConnectionPoolProxy 类**
|“属性”|描述|  
|----------|-----------------|  
|public final boolean getSendTimeAsDatetime()|返回 sendTimeAsDatetime 连接属性的设置。|
|public void setSendTimeAsDatetime (布尔 sendTimeAsDateTimeValue)|修改 sendTimeAsDatetime 连接属性的设置。|
     
  
 **SQLServerDataSource 类**  
  
|“属性”|描述|  
|----------|-----------------|  
|public void setColumnEncryptionSetting(String columnEncryptionSetting)|为数据源对象启用/禁用始终加密功能。<br /><br /> 默认值为“禁用”。|  
|公共字符串 getColumnEncryptionSetting()|检索数据源对象的始终加密功能设置。|
|public void setKeyStoreAuthentication (字符串 keyStoreAuthentication)|设置标识密钥存储的名称。 支持的值是**JavaKeyStorePassword**用于标识 Java 密钥存储。<br/><br/>默认值为 NULL。|
|公共字符串 getKeyStoreAuthentication()|获取数据源对象的 keyStoreAuthentication 设置的值。|
|public void setKeyStoreSecret (字符串 keyStoreSecret)|设置 Java 密钥存储的密码。 密钥存储和密钥的密码必须相同。 请注意必须与设置该 keyStoreAuthentication **JavaKeyStorePassword**。|
|public void setKeyStoreLocation (字符串 keyStoreLocation)|设置包括 Java 密钥存储的文件名称的位置。 请注意必须与设置该 keyStoreAuthentication **JavaKeyStorePassword**。|
|公共字符串 getKeyStoreLocation()|检索为 Java 密钥存储 keyStoreLocation。|
  
 **SQLServerColumnEncryptionJavaKeyStoreProvider 类**  
  
 Java 密钥存储的密钥存储提供程序的实现。 此类支持将存储在 Java 密钥存储中的证书用作列主密钥。  
  
 构造函数  
  
|“属性”|描述|  
|----------|-----------------|  
|公共 SQLServerColumnEncryptionJavaKeyStoreProvider （字符串 keyStoreLocation，char [] keyStoreSecret）|为 Java 密钥存储的密钥存储提供程序。|  
  
 方法  
  
|“属性”|描述|  
|----------|-----------------|  
|public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)|解密列加密密钥的指定加密值。 预期使用带有指定密钥路径的证书并使用指定算法加密该加密值。<br /><br /> **密钥路径的格式应为以下各项之一：**<br /><br /> 指纹：<certificate_thumbprint><br /><br /> 别名：<certificate_alias><br /><br /> （替代 SQLServerColumnEncryptionKeyStoreProvider。 decryptColumnEncryptionKey （字符串、 字符串、 Byte[]).)|  
|public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)|使用带有指定密钥路径的证书并使用指定算法加密列加密密钥。<br /><br /> **密钥路径的格式应为以下各项之一：**<br /><br /> 指纹：<certificate_thumbprint><br /><br /> 别名：<certificate_alias><br /><br /> （替代 SQLServerColumnEncryptionKeyStoreProvider。 encryptColumnEncryptionKey （字符串、 字符串、 Byte[]).)|  
|public void setName （字符串名称）|设置此密钥存储提供程序的名称。|
|public String getName ()|获取此密钥存储提供程序的名称。|
  
 **SQLServerColumnEncryptionAzureKeyVaultProvider 类**  
  
 Azure Key Vault 的密钥存储提供程序的实现。 此类支持使用 Azure 密钥保管库中存储用作列主密钥的密钥。  
  
 构造函数  
  
|“属性”|描述|  
|----------|-----------------|  
|公共 SQLServerColumnEncryptionAzureKeyVaultProvider （字符串 clientId，字符串 clientKey）|Azure 密钥保管库的密钥存储提供程序。  需要提供的标识符和客户端请求该令牌向 Azure 密钥保管库进行身份验证的密钥。|  
  
 方法  
  
|“属性”|描述|  
|----------|-----------------|  
|public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)|解密列加密密钥的指定加密值。 应使用指定的列密钥 IDmaster 密钥并使用指定算法加密该加密值。 <br />（替代 SQLServerColumnEncryptionKeyStoreProvider。 decryptColumnEncryptionKey （字符串、 字符串、 Byte[]).)|  
|public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] columnEncryptionKey)|对列加密密钥，使用指定的列主密钥和使用指定的算法进行加密。 <br />（替代 SQLServerColumnEncryptionKeyStoreProvider。 encryptColumnEncryptionKey （字符串、 字符串、 Byte[]).)|  
|public void setName （字符串名称）|设置此密钥存储提供程序的名称。|
|public String getName ()|获取此密钥存储提供程序的名称。|  
  
  
 **SQLServerKeyVaultAuthenticationCallback 接口**  
  
 此接口包含一种方法进行 Azure 密钥保管库身份验证，这是由用户来实现。  
  
 方法  
  
|“属性”|描述|  
|----------|-----------------|  
|公共字符串 getAccessToken （字符串颁发机构、 字符串资源、 字符串范围）|该方法需要重写。 该方法用于获取访问令牌向 Azure 密钥保管库。|  
  
 **SQLServerColumnEncryptionKeyStoreProvider 类**  
  
 扩展此类以实现自定义密钥存储提供程序。  
  
|“属性”|描述|  
|----------|-----------------|  
|SQLServerColumnEncryptionKeyStoreProvider|所有密钥存储提供程序的基类。 自定义提供程序必须派生自此类并替代其成员函数，然后使用 SQLServerConnection 注册它。 registerColumnEncryptionKeyStoreProviders()。|  
  
 方法  
  
|“属性”|描述|  
|----------|-----------------|  
|public abstract byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)|用于解密列加密密钥的指定加密值的基类方法。 预期使用带有指定密钥路径的列主密钥和指定算法加密该加密值。|  
|public abstract byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[]  columnEncryptionKey)|用于使用带有指定密钥路径的列主密钥并使用指定算法加密列加密密钥的基类算法。|
|公共抽象 void setName （字符串名称）|设置此密钥存储提供程序的名称。|
|公共抽象字符串 getName()|获取此密钥存储提供程序的名称。|  
  
 中的新的或重载方法**SQLServerPreparedStatement**类  
  
|“属性”|描述|  
|----------|-----------------|  
|public void setBigDecimal (int parameterIndex，x，int 精度 BigDecimal int 规模)<br /><br /> public void setObject （int parameterIndex，对象 x，int targetSqlType，整数精度和 int 小数位数）<br /><br /> public void setObject （int parameterIndex，对象 x，SQLType targetSqlType，整数精度，整数小数位数）<br /><br /> public void setTime （int parameterIndex，x，int 规模 java.sql.Time）<br /><br /> public void setTimestamp （int parameterIndex，x，int 规模 java.sql.Timestamp） <br />public void setDateTimeOffset （int parameterIndex，x，int 规模 microsoft.sql.DateTimeOffset）|这些方法重载与精度或小数位数参数和 / 或以特定数据类型的需要精度和小数位数信息支持始终加密。|  
|public void setMoney (int parameterIndex，BigDecimal x)<br /><br /> public void setSmallMoney (int parameterIndex，BigDecimal x)<br /><br /> public void setUniqueIdentifier （int parameterIndex，字符串 guid）<br /><br /> public void setDateTime (int parameterIndex java.sql.Timestamp x)<br /><br /> public void setSmallDateTime (int parameterIndex java.sql.Timestamp x)|这些方法添加为数据类型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime 的支持始终加密。 <br/><br/>请注意，现有 setTimestamp() 方法用于将参数值发送到加密的 datetime2 列。 加密的 datetime 和 smalldatetime 列的新方法 setDateTime() 和 setSmallDateTime() 分别使用。|  
|公共最终 void setBigDecimal （int parameterIndex，BigDecimal x，int 精度、 布尔 forceEncrypt 的 int 小数位数）<br /><br /> 公共最终 void setMoney (x，布尔 forceEncrypt BigDecimal int parameterIndex)<br /><br /> 公共最终 void setSmallMoney (x，布尔 forceEncrypt BigDecimal int parameterIndex)<br /><br /> 公共最终 void setBoolean （int parameterIndex，布尔值 x，布尔 forceEncrypt）<br /><br /> 公共最终 void setByte （int parameterIndex，x，布尔 forceEncrypt 字节）<br /><br /> 公共最终 void setBytes （int parameterIndex，字节 x[]，布尔 forceEncrypt）<br /><br /> 公共最终 void setUniqueIdentifier （int parameterIndex、 guid 字符串、 布尔 forceEncrypt）<br /><br /> 公共最终 void setDouble int parameterIndex、 双精度 x (布尔 forceEncrypt）<br /><br /> 公共最终 void setFloat （int parameterIndex、 浮点数 x，布尔 forceEncrypt）<br /><br /> 公共最终 void setInt （int parameterIndex，int 值，布尔 forceEncrypt）<br /><br /> 公共最终 void setLong （int parameterIndex，长时间 x，布尔 forceEncrypt）<br /><br /> 公共最终 setObject （int parameterIndex，对象 x、 int targetSqlType、 整数精度、 布尔 forceEncrypt 的 int 小数位数）<br /><br /> 公共最终 void setObject （int parameterIndex，对象 x、 SQLType targetSqlType、 整数精度、 布尔 forceEncrypt 的整数小数位数）<br /><br /> 公共最终 void setShort （int parameterIndex，短 x，布尔 forceEncrypt）<br /><br /> 公共最终 void setString (int parameterIndex，字符串 str 布尔 forceEncrypt)<br /><br /> 公共最终 void setNString （int parameterIndex、 字符串值、 布尔 forceEncrypt）<br /><br /> 最终的公共 void setTime (int parameterIndex，x，int 规模 java.sql.Time 布尔 forceEncrypt)<br /><br /> 最终的公共 void setTimestamp (int parameterIndex，x，int 规模 java.sql.Timestamp 布尔 forceEncrypt)<br /><br /> 最终的公共 void setDateTimeOffset (int parameterIndex，x，int 规模 microsoft.sql.DateTimeOffset 布尔 forceEncrypt)<br /><br /> 公共最终 void setDateTime （int parameterIndex，x，布尔 forceEncrypt java.sql.Timestamp）<br /><br /> 公共最终 void setSmallDateTime （int parameterIndex，x，布尔 forceEncrypt java.sql.Timestamp）<br /><br /> 最终的公共 void setDate (int parameterIndex，x，java.util.Calendar cal java.sql.Date 布尔 forceEncrypt)<br /><br /> 最终的公共 void setTime (int parameterIndex，x，java.util.Calendar cal java.sql.Time 布尔 forceEncrypt)<br /><br /> 最终的公共 void setTimestamp (int parameterIndex，x，java.util.Calendar cal java.sql.Timestamp 布尔 forceEncrypt)|将指定参数设置为给定的 Java 值。<br /><br /> 如果布尔 forceEncrypt 设置为 true 时，查询将仅当将参数设置的指定列进行加密，或该语句上连接启用始终加密。<br /><br /> 如果布尔 forceEncrypt 设置为 false，该驱动程序不会强制对参数进行加密。|  
  
 中的新的或重载方法**SQLServerCallableStatement**类  
  
|“属性”|描述|  
|----------|-----------------|  
|public void registerOutParameter （int parameterIndex，int sqlType、 int 精度，int 规模）<br /><br /> public void registerOutParameter(int parameterIndex, SQLType sqlType, int precision, int scale)<br /><br /> public void registerOutParameter （字符串 parameterName，int sqlType、 int 精度，int 规模）<br /><br /> public void registerOutParameter(String parameterName, SQLType sqlType, int precision, int scale)<br />public void setBigDecimal （字符串 parameterName，BigDecimal bd、 int 精度，int 规模）<br /><br /> public void setTime （字符串 parameterName，java.sql.Time t，int 规模）<br /><br /> public void setTimestamp （字符串 parameterName，java.sql.Timestamp t，int 规模）<br /><br /> public void setDateTimeOffset （字符串 parameterName，microsoft.sql.DateTimeOffset t，int 规模）<br/><br/>公共最终 void setObject （字符串 sCol，对象 x，int targetSqlType，整数精度和 int 小数位数）|这些方法重载与精度或小数位数参数和 / 或以特定数据类型的需要精度和小数位数信息支持始终加密。|  
|public void setDateTime (字符串 parameterName，java.sql.Timestamp x)<br /><br /> public void setSmallDateTime (字符串 parameterName，java.sql.Timestamp x)<br /><br /> public void setUniqueIdentifier （字符串参数名称，字符串 guid）<br /><br /> public void setMoney （字符串 parameterName，BigDecimal bd）<br /><br /> public void setSmallMoney （字符串 parameterName，BigDecimal bd）<br/><br/>公共时间戳 getDateTime (int index)<br/><br/>公共时间戳 getDateTime (字符串 sCol)<br/><br/>公共时间戳 getDateTime （int index、 日历 cal）<br/><br/>公共时间戳 getSmallDateTime (int index)<br/><br/>公共时间戳 getSmallDateTime (字符串 sCol)<br/><br/>公共时间戳 getSmallDateTime （int index、 日历 cal）<br/><br/>公共时间戳 getSmallDateTime （字符串名称，日历 cal）<br/><br/>公共 BigDecimal getMoney (int index)<br/><br/>公共 BigDecimal getMoney (字符串 sCol)<br/><br/>公共 BigDecimal getSmallMoney (int index)<br/><br/>公共 BigDecimal getSmallMoney (字符串 sCol)|这些方法添加为数据类型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime 的支持始终加密。 <br/><br/>请注意，现有 setTimestamp() 方法用于将参数值发送到加密的 datetime2 列。 加密的 datetime 和 smalldatetime 列的新方法 setDateTime() 和 setSmallDateTime() 分别使用。|  
|public void setObject （字符串参数名称，对象 o、 int n、 int m，布尔 forceEncrypt）<br /><br /> public void setObject （字符串参数名称、 对象 obj、 SQLType jdbcType、 int 规模、 布尔 forceEncrypt）<br /><br /> public void setDate (字符串 parameterName，x，日历 c java.sql.Date 布尔 forceEncrypt)<br /><br /> public void setTime （字符串 parameterName，java.sql.Time t、 int 规模，布尔 forceEncrypt）<br /><br /> public void setTime (字符串 parameterName，x，日历 c java.sql.Time 布尔 forceEncrypt)<br /><br /> public void setDateTime （字符串 parameterName，x，布尔 forceEncrypt java.sql.Timestamp）<br /><br /> public void setDateTimeOffset （字符串 parameterName、 microsoft.sql.DateTimeOffset t、 int 规模、 布尔 forceEncrypt）<br /><br /> public void setSmallDateTime （字符串 parameterName，x，布尔 forceEncrypt java.sql.Timestamp）<br /><br /> public void setTimestamp （字符串 parameterName，java.sql.Timestamp t、 int 规模，布尔 forceEncrypt）<br /><br /> public void setTimestamp （字符串 parameterName，x，布尔 forceEncrypt java.sql.Timestamp）<br /><br /> public void setUniqueIdentifier （字符串参数名称、 guid 字符串、 布尔 forceEncrypt）<br /><br /> public void setBytes （字符串 parameterName、 byte [] b、 布尔 forceEncrypt）<br /><br /> public void setByte （字符串 parameterName，字节 b，布尔 forceEncrypt）<br /><br /> public void setString （字符串参数名称，字符串 s，布尔 forceEncrypt）<br /><br /> 公共最终 void setNString （字符串参数名称、 字符串值、 布尔 forceEncrypt）<br /><br /> public void setMoney （字符串 parameterName，BigDecimal bd，布尔 forceEncrypt）<br /><br /> public void setSmallMoney （字符串 parameterName，BigDecimal bd，布尔 forceEncrypt）<br /><br /> public void setBigDecimal （字符串 parameterName、 BigDecimal bd、 int 精度、 int 规模、 布尔 forceEncrypt）<br /><br /> public void setDouble （字符串 parameterName、 双线 d，布尔 forceEncrypt）<br /><br /> public void setFloat （字符串 parameterName，float f，布尔 forceEncrypt）<br /><br /> public void setInt (字符串 parameterName，int i，布尔 forceEncrypt)<br /><br /> public void setLong （字符串参数名称，长时间 l，布尔 forceEncrypt）<br /><br /> public void setShort （字符串参数名称，短 s，布尔 forceEncrypt）<br /><br /> public void setBoolean （字符串 parameterNames，布尔值 b，布尔 forceEncrypt）<br/><br/>public void setTimeStamp (字符串 sCol，x，日历 c java.sql.Timestamp 布尔 forceEncrypt)|将指定参数设置为给定的 Java 值。<br /><br /> 如果布尔 forceEncrypt 设置为 true 时，查询将仅当将参数设置的指定列进行加密，或该语句上连接启用始终加密。<br /><br /> 如果布尔 forceEncrypt 设置为 false，该驱动程序不会强制对参数进行加密。|
 

 中的新的或重载方法**SQLServerResultSet**类  
  
|“属性”|描述|  
|----------|-----------------|  
|公共字符串 getUniqueIdentifier （int 的列索引）<br/><br/>公共字符串 getUniqueIdentifier (字符串 columnLabel)<br/><br/>   公共 java.sql.Timestamp getDateTime （int 的列索引） <br/><br/> 公共 java.sql.Timestamp getDateTime (字符串 columnName)   <br/><br/> 公共 java.sql.Timestamp getDateTime （int 的列索引，日历 cal）   <br/><br/>公共 java.sql.Timestamp getDateTime （字符串 colName，日历 cal）    <br/><br/>公共 java.sql.Timestamp getSmallDateTime （int 的列索引）    <br/><br/> 公共 java.sql.Timestamp getSmallDateTime (字符串 columnName)   <br/><br/> 公共 java.sql.Timestamp getSmallDateTime （int 的列索引，日历 cal）   <br/><br/> 公共 java.sql.Timestamp getSmallDateTime （字符串 colName，日历 cal）   <br/><br/>  公共 BigDecimal getMoney （int 的列索引）  <br/><br/> 公共 BigDecimal getMoney (字符串 columnName)   <br/><br/> 公共 BigDecimal getSmallMoney （int 的列索引）   <br/><br/>  公共 BigDecimal getSmallMoney (字符串 columnName)  <br/><br/>public void updateMoney (字符串 columnName，BigDecimal x)    <br/><br/>  public void updateSmallMoney (字符串 columnName，BigDecimal x)  <br/><br/>     public void updateDateTime (int 索引 java.sql.Timestamp x) <br/><br/> public void updateSmallDateTime (int 索引 java.sql.Timestamp x) |这些方法添加为数据类型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime 的支持始终加密。 <br/><br/>请注意，现有 updateTimestamp() 方法用于更新加密的 datetime2 列。 加密的 datetime 和 smalldatetime 列的新方法 updateDateTime() 和 updateSmallDateTime() 分别使用。|
|public void updateBoolean （int index、 布尔值 x，布尔 forceEncrypt）  <br/><br/>  public void updateByte （int 索引，x，布尔 forceEncrypt 字节）  <br/><br/>  public void updateShort （int 索引，短 x，布尔 forceEncrypt）  <br/><br/> public void updateInt （int 索引，x，布尔 forceEncrypt 的 int）   <br/><br/>  public void updateLong int index、 长时间 x (布尔 forceEncrypt）  <br/><br/> public void updateFloat （int index、 浮点数 x，布尔 forceEncrypt）   <br/><br/> public void updateDouble (int index，双精度 x，布尔 forceEncrypt）   <br/><br/> public void updateMoney (x，布尔 forceEncrypt BigDecimal int index)   <br/><br/>  public void updateMoney (x，布尔 forceEncrypt BigDecimal 字符串 columnName)  <br/><br/> public void updateSmallMoney (x，布尔 forceEncrypt BigDecimal int index)   <br/><br/>  public void updateSmallMoney (x，布尔 forceEncrypt BigDecimal 字符串 columnName)  <br/><br/> public void updateBigDecimal （int 索引，x，整数精度 BigDecimal，整数规模，布尔 forceEncrypt）   <br/><br/>  public void updateString （int 的列索引，字符串 stringValue，布尔 forceEncrypt）  <br/><br/>  public void updateNString （int 的列索引，字符串结尾，布尔 forceEncrypt）  <br/><br/>  public void updateNString （字符串 columnLabel，字符串结尾，布尔 forceEncrypt）  <br/><br/> public void updateBytes （int index、 字节 x[]、 布尔 forceEncrypt）   <br/><br/>  public void updateDate （int 索引，x，布尔 forceEncrypt java.sql.Date）  <br/><br/> public void updateTime (int 索引，x，整数规模 java.sql.Time 布尔 forceEncrypt)   <br/><br/> public void updateTimestamp (int 索引，x，int 规模 java.sql.Timestamp 布尔 forceEncrypt)   <br/><br/> public void updateDateTime (int 索引，x，整数规模 java.sql.Timestamp 布尔 forceEncrypt)   <br/><br/> public void updateSmallDateTime (int 索引，x，整数规模 java.sql.Timestamp 布尔 forceEncrypt)   <br/><br/>  public void updateDateTimeOffset (int 索引，x，整数规模 microsoft.sql.DateTimeOffset 布尔 forceEncrypt)  <br/><br/> public void updateUniqueIdentifier (int index、 x，布尔 forceEncrypt 字符串)    <br/><br/>  public void updateObject （int 索引，对象 x、 int 精度、 布尔 forceEncrypt 的 int 小数位数）  <br/><br/>  public void updateObject （int index、 对象 obj、 SQLType targetSqlType、 int 规模、 布尔 forceEncrypt）  <br/><br/> public void updateBoolean （字符串 columnName、 布尔值 x，布尔 forceEncrypt）    <br/><br/>  public void updateByte （字符串 columnName，x，布尔 forceEncrypt 字节）  <br/><br/>  public void updateShort （字符串列名称，短 x，布尔 forceEncrypt）  <br/><br/> public void updateInt （字符串 columnName，x，布尔 forceEncrypt 的 int）   <br/><br/>   public void updateLong （字符串 columnName、 长时间 x、 布尔 forceEncrypt） <br/><br/>  public void updateFloat （字符串 columnName、 浮点数 x，布尔 forceEncrypt）  <br/><br/>  public void updateDouble 字符串 columnName、 双精度 x (布尔 forceEncrypt）  <br/><br/> public void updateBigDecimal (x，布尔 forceEncrypt BigDecimal 字符串 columnName)   <br/><br/>  public void updateBigDecimal （字符串 columnName，x，整数精度 BigDecimal，整数规模，布尔 forceEncrypt）  <br/><br/> public void updateString （字符串列名称，字符串 x，布尔 forceEncrypt）   <br/><br/>  （字符串 columnName、 字节 x[]、 布尔 forceEncrypt） 的公共 void updateBytes  <br/><br/> public void updateDate （字符串 columnName，x，布尔 forceEncrypt java.sql.Date）   <br/><br/>  public void updateTime (字符串 columnName，x，int 规模 java.sql.Time 布尔 forceEncrypt)  <br/><br/>  public void updateTimestamp (字符串 columnName，x，int 规模 java.sql.Timestamp 布尔 forceEncrypt)  <br/><br/> public void updateDateTime (字符串 columnName，x，int 规模 java.sql.Timestamp 布尔 forceEncrypt)   <br/><br/>  public void updateSmallDateTime (字符串 columnName，x，int 规模 java.sql.Timestamp 布尔 forceEncrypt)  <br/><br/>  public void updateDateTimeOffset (字符串 columnName、 x，int 规模 microsoft.sql.DateTimeOffset 布尔 forceEncrypt)  <br/><br/>  public void updateUniqueIdentifier （字符串列名称，字符串 x，布尔 forceEncrypt）<br/><br/>public void updateObject （字符串列名称，对象 x、 int 精度、 布尔 forceEncrypt 的 int 小数位数）<br/><br/>public void updateObject （字符串列名称、 对象 obj、 SQLType targetSqlType、 int 规模、 布尔 forceEncrypt）|为给定的 java 值更新指定的列。<br/><br/>如果布尔 forceEncrypt 设置为 true，列将仅设置如果对其进行加密，并且启用了始终加密的连接上或在语句上。<br/><br/>如果布尔 forceEncrypt 设置为 false，该驱动程序不会强制对参数进行加密。|

  
中的新类型**microsoft.sql.Types**类
|“属性”|描述|  
|----------|-----------------|  
|DATETIME、 SMALLDATETIME、 MONEY、 SMALLMONEY、 GUID|发送到的参数值时为目标 SQL 类型使用这些类型**加密**datetime、 smalldatetime、 money、 smallmoney、 使用 setObject()/updateObject() API 方法的唯一标识符列。|  
  
  
 **SQLServerStatementColumnEncryptionSetting 枚举**  
  
 指定将如何发送和接收时读取和写入加密的列数据。 根据特定的查询，可能会跳过 Always Encrypted 驱动程序的处理使用非加密列时可减少性能影响。 请注意，这些设置不能用于绕过加密以及获取纯文本数据的访问权限。  
  
 **语法**  
  
```java
Public enum  SQLServerStatementColumnEncryptionSetting  
```  
  
 **成员**  
  
|“属性”|描述|  
|----------|-----------------|  
|UseConnectionSetting|指定该命令应默认为连接字符串中的始终加密设置。|  
|已启用|该查询启用始终加密。|  
|ResultSetOnly|指定驱动程序中的 Always Encrypted 例程应处理该命令的结果。 该命令不具有要求加密任何参数时，请使用此值。|  
|禁用|该查询禁用 Always Encrypted。|  
  
 AE 的语句级别设置添加到 SQLServerConnection 类和 SQLServerConnectionPoolProxy 类。 这些类中的以下方法重载使用新的设置。  
  
|“属性”|描述|  
|----------|-----------------|  
|公共语句 createStatement （n 类型 int，int nConcur、 int statementHoldability，SQLServerStatementColumnEncryptionSetting stmtColEncSetting）|创建语句对象将生成结果集对象使用给定的类型、 并发、 保持能力和列加密设置。|  
|公共 CallableStatement prepareCall （字符串 sql、 n 类型 int、 int nConcur、 int statementHoldability、 SQLServerStatementColumnEncryptionSetting stmtColEncSetiing）|使用给定的列加密设置，将生成具有给定的类型、 并发和保持能力的结果集对象创建 CallableStatement 对象。|  
|公共 PreparedStatement prepareStatement （字符串 sql，int autogeneratedKeys，SQLServerStatementColumnEncryptionSetting stmtColEncSetting）|使用给定的列加密设置，可以检索自动生成的键创建 PreparedStatement 对象。|  
|公共 PreparedStatement prepareStatement （字符串 sql，字符串 [] columnNames，SQLServerStatementColumnEncryptionSetting stmtColEncSetting）|使用给定的列加密设置，将生成结果集对象使用给定的列名称创建 PreparedStatement 对象。|  
|公共 PreparedStatement prepareStatement （字符串 sql，int [] columnIndexes、 SQLServerStatementColumnEncryptionSetting stmtColEncSetting|使用给定的列加密设置，将生成结果集对象使用给定的列索引创建 PreparedStatement 对象。|  
|公共 PreparedStatement prepareStatement （字符串 sql、 n 类型 int、 int nConcur、 int nHold、 SQLServerStatementColumnEncryptionSetting stmtColEncSetting）|使用给定的列加密设置，将生成具有给定的类型、 并发和保持能力的结果集对象创建 PreparedStatement 对象。|  
  
> [!NOTE]  
>  如果查询禁用 Always Encrypted，并且查询有参数需要加密 （对应于参数加密列），则查询将失败。  
>   
>  如果查询禁用 Always Encrypted，查询将返回从加密列的结果，查询将返回加密的值。 加密的值将具有 varbinary 数据类型。  
  
 ## <a name="see-also"></a>另请参阅  
 [对 JDBC 驱动程序使用始终加密](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
  

