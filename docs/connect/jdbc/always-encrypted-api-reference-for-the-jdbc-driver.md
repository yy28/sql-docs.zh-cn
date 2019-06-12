---
title: JDBC 驱动程序的 Always Encrypted API 参考 | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6962a2aa-9508-4d4f-a78c-905e2bc68615
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 36ccbdddde5276bedffe3271a541875f1e555df3
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66770481"
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
|新方法：<br /><br /> `public static void setColumnEncryptionTrustedMasterKeyPaths(Map<String, List\<String>> trustedKeyPaths)`<br /><br /> `public static void updateColumnEncryptionTrustedMasterKeyPaths(String server, List\<String> trustedKeyPaths)`<br /><br /> `public static void removeColumnEncryptionTrustedMasterKeyPaths(String server)`|允许为数据库服务器设置/更新/删除受信任的密钥路径的列表。 如果在处理应用程序查询时，驱动程序收到不在列表上的密钥路径，则查询将失败。 此属性提供针对安全攻击的额外保护，这些攻击涉及到发送伪造密钥路径的受损 SQL Server，这可能导致泄露密钥存储凭据。|  
|新方法：<br /><br /> `public static Map<String, List\<String>> getColumnEncryptionTrustedMasterKeyPaths()`|为数据库服务器返回受信任的密钥路径的列表。|  
|新方法：<br /><br /> `public static void registerColumnEncryptionKeyStoreProviders (Map\<String, SQLServerColumnEncryptionKeyStoreProvider> clientKeyStoreProviders)`|允许你注册自定义密钥存储提供程序。 它是一个将密钥存储提供程序名称映射到密钥存储提供程序实现的字典。<br /><br /> 若要使用 JVM 密钥存储，需要使用 JVM 密钥存储凭据实例化 SQLServerColumnEncryptionJVMKeyStoreProvider 对象，并使用驱动程序注册它。 此提供程序的名称必须为“MSSQL_JVM_KEYSTORE”。<br /><br /> 若要使用 Azure 密钥保管库存储区，需要实例化 SQLServerColumnEncryptionAzureKeyStoreProvider 对象并将其注册的驱动程序。 为此提供程序名称必须是 AZURE_KEY_VAULT。|
|`public final boolean getSendTimeAsDatetime()`|返回 sendTimeAsDatetime 连接属性的设置。|
|`public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)`|修改 sendTimeAsDatetime 连接属性的设置。|

 **SQLServerConnectionPoolProxy 类**
 
|“属性”|描述|  
|----------|-----------------|  
|`public final boolean getSendTimeAsDatetime()` | 返回 sendTimeAsDatetime 连接属性的设置。|
|`public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)` | 修改 sendTimeAsDatetime 连接属性的设置。|
     
  
 **SQLServerDataSource 类**  
  
|“属性”|描述|  
|----------|-----------------|  
|`public void setColumnEncryptionSetting(String columnEncryptionSetting)`|为数据源对象启用/禁用始终加密功能。<br /><br /> 默认值为“禁用”。|  
|`public String getColumnEncryptionSetting()`|检索数据源对象的始终加密功能设置。|
|`public void setKeyStoreAuthentication(String keyStoreAuthentication)`|设置标识密钥存储的名称。 支持的值是**JavaKeyStorePassword**用于标识 Java 密钥存储。<br/><br/>默认值为 NULL。|
|`public String getKeyStoreAuthentication()`|获取数据源对象的 keyStoreAuthentication 设置的值。|
|`public void setKeyStoreSecret(String keyStoreSecret)`|设置 Java 密钥存储的密码。 密钥存储和密钥的密码必须相同。 请注意必须与设置该 keyStoreAuthentication **JavaKeyStorePassword**。|
|`public void setKeyStoreLocation(String keyStoreLocation)`|设置包括 Java 密钥存储的文件名称的位置。 请注意必须与设置该 keyStoreAuthentication **JavaKeyStorePassword**。|
|`public String getKeyStoreLocation()`|检索为 Java 密钥存储 keyStoreLocation。|
  
 **SQLServerColumnEncryptionJavaKeyStoreProvider 类**  
  
 Java 密钥存储的密钥存储提供程序的实现。 此类支持将存储在 Java 密钥存储中的证书用作列主密钥。  
  
 构造函数  
  
|“属性”|描述|  
|----------|-----------------|  
|`public SQLServerColumnEncryptionJavaKeyStoreProvider (String keyStoreLocation, char[] keyStoreSecret)`|为 Java 密钥存储的密钥存储提供程序。|  
  
 方法  
  
|“属性”|描述|  
|----------|-----------------|  
|`public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)`|解密列加密密钥的指定加密值。 预期使用带有指定密钥路径的证书并使用指定算法加密该加密值。<br /><br /> **密钥路径的格式应为以下各项之一：**<br /><br /> 指纹：<certificate_thumbprint><br /><br /> 别名：<certificate_alias><br /><br /> （替代 SQLServerColumnEncryptionKeyStoreProvider。 decryptColumnEncryptionKey(String, String, Byte[])。）|  
|`public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)`|使用带有指定密钥路径的证书并使用指定算法加密列加密密钥。<br /><br /> **密钥路径的格式应为以下各项之一：**<br /><br /> 指纹：<certificate_thumbprint><br /><br /> 别名：<certificate_alias><br /><br /> （替代 SQLServerColumnEncryptionKeyStoreProvider。 encryptColumnEncryptionKey(String, String, Byte[])。）|  
|`public void setName (String name)`|设置此密钥存储提供程序的名称。|
|`public String getName ()`|获取此密钥存储提供程序的名称。|
  
 **SQLServerColumnEncryptionAzureKeyVaultProvider 类**  
  
 Azure Key Vault 的密钥存储提供程序的实现。 此类支持使用 Azure 密钥保管库中存储用作列主密钥的密钥。  
  
 构造函数  
  
|“属性”|描述|  
|----------|-----------------|  
|`public SQLServerColumnEncryptionAzureKeyVaultProvider (String clientId, String clientKey)`|Azure 密钥保管库的密钥存储提供程序。  需要提供的标识符和客户端请求该令牌向 Azure 密钥保管库进行身份验证的密钥。|  
  
 方法  
  
|“属性”|描述|  
|----------|-----------------|  
| `public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)` | Decryptes 已加密的列加密密钥 (CEK)。 使用指定的主密钥路径中的非对称密钥的 RSA 加密算法来实现此解密。<br />（替代 SQLServerColumnEncryptionKeyStoreProvider。 decryptColumnEncryptionKey(String, String, Byte[])。） |  
| `public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] columnEncryptionKey)` | 对列加密密钥，通过向指定的算法的指定的列主密钥进行加密。<br />（替代 SQLServerColumnEncryptionKeyStoreProvider。 encryptColumnEncryptionKey(String, String, Byte[])。） |  
|`public void setName (String name)`|设置此密钥存储提供程序的名称。|
|`public String getName ()`|获取此密钥存储提供程序的名称。|  
  
  
 **SQLServerKeyVaultAuthenticationCallback 接口**  
  
 此接口包含一种方法进行 Azure 密钥保管库身份验证，这是由用户来实现。  
  
 方法  
  
|“属性”|描述|  
|----------|-----------------|  
|`public String getAccessToken(String authority, String resource, String scope);`|该方法需要重写。 该方法用于获取访问令牌向 Azure 密钥保管库。|  
  
 **SQLServerColumnEncryptionKeyStoreProvider 类**  
  
 扩展此类以实现自定义密钥存储提供程序。  
  
|“属性”|描述|  
|----------|-----------------|  
|SQLServerColumnEncryptionKeyStoreProvider|所有密钥存储提供程序的基类。 自定义提供程序必须派生自此类并替代其成员函数，然后使用 SQLServerConnection 注册它。 registerColumnEncryptionKeyStoreProviders()。|  
  
 方法  
  
|“属性”|描述|  
|----------|-----------------|  
|`public abstract byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)`|用于解密列加密密钥的指定加密值的基类方法。 预期使用带有指定密钥路径的列主密钥和指定算法加密该加密值。|  
|`public abstract byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[]  columnEncryptionKey)`|用于使用带有指定密钥路径的列主密钥并使用指定算法加密列加密密钥的基类算法。|
|`public abstract void setName(String name)`|设置此密钥存储提供程序的名称。|
|`public abstract String getName()`|获取此密钥存储提供程序的名称。|  
  
 中的新的或重载方法**SQLServerPreparedStatement**类  
  
|“属性”|描述|  
|----------|-----------------|  
|`public void setBigDecimal(int parameterIndex, BigDecimal x, int precision, int scale)`<br /><br /> `public void setObject(int parameterIndex, Object x, int targetSqlType, Integer precision, int scale)`<br /><br /> `public void setObject(int parameterIndex, Object x, SQLType targetSqlType, Integer precision, Integer scale)`<br /><br /> `public void setTime(int parameterIndex, java.sql.Time x, int scale)`<br /><br /> `public void setTimestamp(int parameterIndex, java.sql.Timestamp x, int scale)` <br />`public void setDateTimeOffset(int parameterIndex, microsoft.sql.DateTimeOffset x, int scale)`|这些方法重载与精度或小数位数参数和 / 或以特定数据类型的需要精度和小数位数信息支持始终加密。|  
|`public void setMoney(int parameterIndex, BigDecimal x)`<br /><br /> `public void setSmallMoney(int parameterIndex, BigDecimal x)`<br /><br /> `public void setUniqueIdentifier(int parameterIndex, String guid)`<br /><br /> `public void setDateTime(int parameterIndex, java.sql.Timestamp x)`<br /><br /> `public void setSmallDateTime(int parameterIndex, java.sql.Timestamp x)`|这些方法添加为数据类型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime 的支持始终加密。 <br/><br/>请注意，现有`setTimestamp()`方法用于将参数值发送到加密的 datetime2 列。 对于加密的 datetime 和 smalldatetime 列使用的新方法`setDateTime()`和`setSmallDateTime()`分别。|  
|`public final void setBigDecimal(int parameterIndex, BigDecimal x, int precision, int scale, boolean forceEncrypt)`<br /><br /> `public final void setMoney(int parameterIndex, BigDecimal x, boolean forceEncrypt)`<br /><br /> `public final void setSmallMoney(int parameterIndex, BigDecimal x, boolean forceEncrypt)`<br /><br /> `public final void setBoolean(int parameterIndex, boolean x, boolean forceEncrypt)`<br /><br /> `public final void setByte(int parameterIndex, byte x, boolean forceEncrypt)`<br /><br /> `public final void setBytes(int parameterIndex, byte x[], boolean forceEncrypt)`<br /><br /> `public final void setUniqueIdentifier(int parameterIndex, String guid, boolean forceEncrypt)`<br /><br /> `public final void setDouble(int parameterIndex, double x, boolean forceEncrypt)`<br /><br /> `public final void setFloat(int parameterIndex, float x, boolean forceEncrypt)`<br /><br /> `public final void setInt(int parameterIndex, int value, boolean forceEncrypt)`<br /><br /> `public final void setLong(int parameterIndex, long x, boolean forceEncrypt)`<br /><br /> `public final setObject(int parameterIndex, Object x, int targetSqlType, Integer precision, int scale, boolean forceEncrypt)`<br /><br /> `public final void setObject(int parameterIndex, Object x, SQLType targetSqlType, Integer precision, Integer scale, boolean forceEncrypt)`<br /><br /> `public final void setShort(int parameterIndex, short x, boolean forceEncrypt)`<br /><br /> `public final void setString(int parameterIndex, String str, boolean forceEncrypt)`<br /><br /> `public final void setNString(int parameterIndex, String value, boolean forceEncrypt)`<br /><br /> `public final void setTime(int parameterIndex, java.sql.Time x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setTimestamp(int parameterIndex, java.sql.Timestamp x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setDateTimeOffset(int parameterIndex, microsoft.sql.DateTimeOffset x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setDateTime(int parameterIndex, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public final void setSmallDateTime(int parameterIndex, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public final void setDate(int parameterIndex, java.sql.Date x, java.util.Calendar cal, boolean forceEncrypt)`<br /><br /> `public final void setTime(int parameterIndex, java.sql.Time x, java.util.Calendar cal, boolean forceEncrypt)`<br /><br /> `public final void setTimestamp(int parameterIndex, java.sql.Timestamp x, java.util.Calendar cal, boolean forceEncrypt)`|将指定参数设置为给定的 Java 值。<br /><br /> 如果布尔 forceEncrypt 设置为 true 时，查询将仅当将参数设置的指定列进行加密，或该语句上连接启用始终加密。<br /><br /> 如果布尔 forceEncrypt 设置为 false，该驱动程序不会强制对参数进行加密。|  
  
 中的新的或重载方法**SQLServerCallableStatement**类  
  
|“属性”|描述|  
|----------|-----------------|  
|`public void registerOutParameter(int parameterIndex, int sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(int parameterIndex, SQLType sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(String parameterName, int sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(String parameterName, SQLType sqlType, int precision, int scale)`<br />`public void setBigDecimal(String parameterName, BigDecimal bd, int precision, int scale)`<br /><br /> `public void setTime(String parameterName, java.sql.Time t, int scale)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp t, int scale)`<br /><br /> `public void setDateTimeOffset(String parameterName, microsoft.sql.DateTimeOffset t, int scale)`<br/><br/>`public final void setObject(String sCol, Object x, int targetSqlType, Integer precision, int scale)`|这些方法重载与精度或小数位数参数和 / 或以特定数据类型的需要精度和小数位数信息支持始终加密。|  
|`public void setDateTime(String parameterName, java.sql.Timestamp x)`<br /><br /> `public void setSmallDateTime(String parameterName, java.sql.Timestamp x)`<br /><br /> `public void setUniqueIdentifier(String parameterName, String guid)`<br /><br /> `public void setMoney(String parameterName, BigDecimal bd)`<br /><br /> `public void setSmallMoney(String parameterName, BigDecimal bd)`<br/><br/>`public Timestamp getDateTime(int index)`<br/><br/>`public Timestamp getDateTime(String sCol)`<br/><br/>`public Timestamp getDateTime(int index, Calendar cal)`<br/><br/>`public Timestamp getSmallDateTime(int index)`<br/><br/>`public Timestamp getSmallDateTime(String sCol)`<br/><br/>`public Timestamp getSmallDateTime(int index, Calendar cal)`<br/><br/>`public Timestamp getSmallDateTime(String name, Calendar cal)`<br/><br/>`public BigDecimal getMoney(int index)`<br/><br/>`public BigDecimal getMoney(String sCol)`<br/><br/>`public BigDecimal getSmallMoney(int index)`<br/><br/>`public BigDecimal getSmallMoney(String sCol)`|这些方法添加为数据类型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime 的支持始终加密。 <br/><br/>请注意，现有`setTimestamp()`方法用于将参数值发送到加密的 datetime2 列。 对于加密的 datetime 和 smalldatetime 列使用的新方法`setDateTime()`和`setSmallDateTime()`分别。|  
|`public void setObject(String parameterName, Object o, int n, int m, boolean forceEncrypt)`<br /><br /> `public void setObject(String parameterName, Object obj, SQLType jdbcType, int scale, boolean forceEncrypt)`<br /><br /> `public void setDate(String parameterName, java.sql.Date x, Calendar c, boolean forceEncrypt)`<br /><br /> `public void setTime(String parameterName, java.sql.Time t, int scale, boolean forceEncrypt)`<br /><br /> `public void setTime(String parameterName, java.sql.Time x, Calendar c, boolean forceEncrypt)`<br /><br /> `public void setDateTime(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setDateTimeOffset(String parameterName, microsoft.sql.DateTimeOffset t, int scale, boolean forceEncrypt)`<br /><br /> `public void setSmallDateTime(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp t, int scale, boolean forceEncrypt)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setUniqueIdentifier(String parameterName, String guid, boolean forceEncrypt)`<br /><br /> `public void setBytes(String parameterName, byte[] b, boolean forceEncrypt)`<br /><br /> `public void setByte(String parameterName, byte b, boolean forceEncrypt)`<br /><br /> `public void setString(String parameterName, String s, boolean forceEncrypt)`<br /><br /> `public final void setNString(String parameterName, String value, boolean forceEncrypt)<br /><br /> public void setMoney(String parameterName, BigDecimal bd, boolean forceEncrypt)`<br /><br /> `public void setSmallMoney(String parameterName, BigDecimal bd, boolean forceEncrypt)`<br /><br /> `public void setBigDecimal(String parameterName, BigDecimal bd, int precision, int scale, boolean forceEncrypt)`<br /><br /> `public void setDouble(String parameterName, double d, boolean forceEncrypt)`<br /><br /> `public void setFloat(String parameterName, float f, boolean forceEncrypt)`<br /><br /> `public void setInt(String parameterName, int i, boolean forceEncrypt)`<br /><br /> `public void setLong(String parameterName, long l, boolean forceEncrypt)`<br /><br /> `public void setShort(String parameterName, short s, boolean forceEncrypt)`<br /><br /> `public void setBoolean(String parameterNames, boolean b, boolean forceEncrypt)`<br/><br/>`public void setTimeStamp(String sCol, java.sql.Timestamp x, Calendar c, Boolean forceEncrypt)`|将指定参数设置为给定的 Java 值。<br /><br /> 如果布尔 forceEncrypt 设置为 true 时，查询将仅当将参数设置的指定列进行加密，或该语句上连接启用始终加密。<br /><br /> 如果布尔 forceEncrypt 设置为 false，该驱动程序不会强制对参数进行加密。|
 

 中的新的或重载方法**SQLServerResultSet**类  
  
|“属性”|描述|  
|----------|-----------------|  
|`public String getUniqueIdentifier(int columnIndex)`<br/><br/>`public String getUniqueIdentifier(String columnLabel)`<br/><br/>   `public java.sql.Timestamp getDateTime(int columnIndex)` <br/><br/> `public java.sql.Timestamp getDateTime(String columnName)`   <br/><br/> `public java.sql.Timestamp getDateTime(int columnIndex, Calendar cal)`   <br/><br/>`public java.sql.Timestamp getDateTime(String colName, Calendar cal)`    <br/><br/>`public java.sql.Timestamp getSmallDateTime(int columnIndex)`    <br/><br/> `public java.sql.Timestamp getSmallDateTime(String columnName)`   <br/><br/> `public java.sql.Timestamp getSmallDateTime(int columnIndex, Calendar cal)`   <br/><br/> `public java.sql.Timestamp getSmallDateTime(String colName, Calendar cal)`   <br/><br/>  `public BigDecimal getMoney(int columnIndex)`  <br/><br/> `public BigDecimal getMoney(String columnName)`   <br/><br/> `public BigDecimal getSmallMoney(int columnIndex)`   <br/><br/>  `public BigDecimal getSmallMoney(String columnName)`  <br/><br/>`public void updateMoney(String columnName, BigDecimal x)`    <br/><br/>  `public void updateSmallMoney(String columnName, BigDecimal x)`  <br/><br/>     `public void updateDateTime(int index, java.sql.Timestamp x)` <br/><br/> `public void updateSmallDateTime(int index, java.sql.Timestamp x)` |这些方法添加为数据类型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime 的支持始终加密。 <br/><br/>请注意，现有`updateTimestamp()`方法用于更新加密的 datetime2 列。 对于加密的 datetime 和 smalldatetime 列使用的新方法`updateDateTime()`和`updateSmallDateTime()`分别。|
|`public void updateBoolean(int index, boolean x, boolean forceEncrypt)`  <br/><br/>  `public void updateByte(int index, byte x, boolean forceEncrypt)`  <br/><br/>  `public void updateShort(int index, short x, boolean forceEncrypt)`  <br/><br/> `public void updateInt(int index, int x, boolean forceEncrypt)`   <br/><br/>  `public void updateLong(int index, long x, boolean forceEncrypt)`  <br/><br/> `public void updateFloat(int index, float x, boolean forceEncrypt)`   <br/><br/> `public void updateDouble(int index, double x, boolean forceEncrypt)`   <br/><br/> `public void updateMoney(int index, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateMoney(String columnName, BigDecimal x, boolean forceEncrypt)`  <br/><br/> `public void updateSmallMoney(int index, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateSmallMoney(String columnName, BigDecimal x, boolean forceEncrypt)`  <br/><br/> `public void updateBigDecimal(int index, BigDecimal x, Integer precision, Integer scale, boolean forceEncrypt)`   <br/><br/>  `public void updateString(int columnIndex, String stringValue, boolean forceEncrypt)`  <br/><br/>  `public void updateNString(int columnIndex, String nString, boolean forceEncrypt)`  <br/><br/>  `public void updateNString(String columnLabel, String nString, boolean forceEncrypt)`  <br/><br/> `public void updateBytes(int index, byte x[], boolean forceEncrypt)   <br/><br/>  public void updateDate(int index, java.sql.Date x, boolean forceEncrypt)`  <br/><br/> `public void updateTime(int index, java.sql.Time x, Integer scale, boolean forceEncrypt)`   <br/><br/> `public void updateTimestamp(int index, java.sql.Timestamp x, int scale, boolean forceEncrypt)`   <br/><br/> `public void updateDateTime(int index, java.sql.Timestamp x, Integer scale, boolean forceEncrypt)`   <br/><br/> `public void updateSmallDateTime(int index, java.sql.Timestamp x, Integer scale, boolean forceEncrypt)`   <br/><br/>  `public void updateDateTimeOffset(int index, microsoft.sql.DateTimeOffset x, Integer scale, boolean forceEncrypt)`  <br/><br/> `public void updateUniqueIdentifier(int index, String x, boolean forceEncrypt)`    <br/><br/>  `public void updateObject(int index, Object x, int precision, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateObject(int index, Object obj, SQLType targetSqlType, int scale, boolean forceEncrypt)`  <br/><br/> `public void updateBoolean(String columnName, boolean x, boolean forceEncrypt)`    <br/><br/>  `public void updateByte(String columnName, byte x, boolean forceEncrypt)`  <br/><br/>  `public void updateShort(String columnName, short x, boolean forceEncrypt)`  <br/><br/> `public void updateInt(String columnName, int x, boolean forceEncrypt)`   <br/><br/>   `public void updateLong(String columnName, long x, boolean forceEncrypt)` <br/><br/>  `public void updateFloat(String columnName, float x, boolean forceEncrypt)`  <br/><br/>  `public void updateDouble(String columnName, double x, boolean forceEncrypt)  <br/><br/> public void updateBigDecimal(String columnName, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateBigDecimal(String columnName, BigDecimal x, Integer precision, Integer scale, boolean forceEncrypt)`  <br/><br/> `public void updateString(String columnName, String x, boolean forceEncrypt)`   <br/><br/>  `public void updateBytes(String columnName, byte x[], boolean forceEncrypt)`  <br/><br/> `public void updateDate(String columnName, java.sql.Date x, boolean forceEncrypt)`   <br/><br/>  `public void updateTime(String columnName, java.sql.Time x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateTimestamp(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`  <br/><br/> `public void updateDateTime(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`   <br/><br/>  `public void updateSmallDateTime(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateDateTimeOffset(String columnName, microsoft.sql.DateTimeOffset x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateUniqueIdentifier(String columnName, String x, boolean forceEncrypt)`<br/><br/>`public void updateObject(String columnName, Object x, int precision, int scale, boolean forceEncrypt)`<br/><br/>`public void updateObject(String columnName, Object obj, SQLType targetSqlType, int scale, boolean forceEncrypt)`|为给定的 java 值更新指定的列。<br/><br/>如果布尔 forceEncrypt 设置为 true，列将仅设置如果对其进行加密，并且启用了始终加密的连接上或在语句上。<br/><br/>如果布尔 forceEncrypt 设置为 false，该驱动程序不会强制对参数进行加密。|

  
中的新类型**microsoft.sql.Types**类

|“属性”|描述|  
|----------|-----------------|  
|DATETIME、 SMALLDATETIME、 MONEY、 SMALLMONEY、 GUID|发送到的参数值时为目标 SQL 类型使用这些类型**加密**datetime、 smalldatetime、 money、 smallmoney、 uniqueidentifier 列使用`setObject()/updateObject()`API 方法。|  
  
  
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
|`public Statement createStatement(int nType, int nConcur, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|创建语句对象将生成结果集对象使用给定的类型、 并发、 保持能力和列加密设置。|  
|`public CallableStatement prepareCall(String sql, int nType, int nConcur, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetiing)`|使用给定的列加密设置，将生成具有给定的类型、 并发和保持能力的结果集对象创建 CallableStatement 对象。|  
|`public PreparedStatement prepareStatement(String sql, int autogeneratedKeys, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|使用给定的列加密设置，可以检索自动生成的键创建 PreparedStatement 对象。|  
|`public PreparedStatement prepareStatement(String sql, String[] columnNames, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|使用给定的列加密设置，将生成结果集对象使用给定的列名称创建 PreparedStatement 对象。|  
|`public PreparedStatement prepareStatement(String sql, int[] columnIndexes, SQLServerStatementColumnEncryptionSetting stmtColEncSetting`|使用给定的列加密设置，将生成结果集对象使用给定的列索引创建 PreparedStatement 对象。|  
|`public PreparedStatement prepareStatement(String sql, int nType, int nConcur, int nHold, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|使用给定的列加密设置，将生成具有给定的类型、 并发和保持能力的结果集对象创建 PreparedStatement 对象。|  
  
> [!NOTE]  
>  如果查询禁用 Always Encrypted，并且查询有参数需要加密 （对应于参数加密列），则查询将失败。  
>   
>  如果查询禁用 Always Encrypted，查询将返回从加密列的结果，查询将返回加密的值。 加密的值将具有 varbinary 数据类型。  
  
 ## <a name="see-also"></a>另请参阅  
 [对 JDBC 驱动程序使用始终加密](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
  

