---
title: 了解数据类型转换 |Microsoft 文档
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
ms.topic: conceptual
ms.assetid: 98fa7488-aac3-45b4-8aa4-83ed6ab638b4
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 718d2777fe25896511f9672f3806438958b8e6cc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="understanding-data-type-conversions"></a>了解数据类型转换
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  为了便于的 Java 编程语言到的数据类型转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供所需的 JDBC 规范的数据类型转换。 为更大的灵活性，所有类型都都可以与其他转换**对象**，**字符串**，和**byte []** 数据类型。  
  
## <a name="getter-method-conversions"></a>Getter 方法转换  
 基于[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型，以下图表包含 get 的 JDBC 驱动程序的转换映射\<类型 > （） 方法的[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)类，并且 get支持的转换\<类型 > 方法[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类。  
  
 ![JDBCGetterConversions](../../connect/jdbc/media/jdbcgetterconversions.gif "JDBCGetterConversions")  
  
 JDBC Driver 的 getter 方法支持三类转换：  
  
-   **非有损 (x)**： 对于情况 getter 类型相同的转换或小于基础的服务器类型。 例如，当调用 getBigDecimal 基础的服务器十进制列，则不必进行转换。  
  
-   **转换后 (y)**： 到 Java 语言类型转换是正则并遵循 Java 语言转换规则的位置从数字服务器类型的转换。 对于这些转换，总是直接截取有效位数（从不四舍五入），而溢出则按目标类型取模处理，以较小者为准。 例如，在基础调用 getInt**十进制**包含"1.9999"列将返回"1"，或者，如果基础**十进制**值是"3000000000"则**int**值为"-1294967296"溢出。  
  
-   **数据相关的 (z)**： 从基础字符类型为数值类型的转换要求字符类型包含可以转换为该类型的值。 不执行其他转换。 如果值对于 getter 类型过大，则该值无效。 例如，如果在包含"53"varchar(50) 列上调用 getInt，则返回的值是为**int**; 但如果基础值为"xyz"或"3000000000"，将引发错误。  
  
 如果在上调用 getString**二进制**， **varbinary**， **varbinary （max)**，或**映像**列的数据类型，则返回值为十六进制字符串值。  
  
## <a name="updater-method-conversions"></a>Updater 方法转换  
 对于 Java 类型化数据传递给更新\<类型 > （） 方法的[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)类，将应用以下转换。  
  
 ![JDBCUpdaterConversions](../../connect/jdbc/media/jdbc_jdbcupdatterconversions.gif "JDBCUpdaterConversions")  
  
 JDBC Driver 的 updater 方法支持三类转换：  
  
-   **非有损 (x)**： 的情况下，更新程序类型相同的转换或小于基础的服务器类型。 例如，对基础服务器十进制数列调用 updateBigDecimal 时，无需进行转换。  
  
-   **转换后 (y)**： 到 Java 语言类型转换是正则并遵循 Java 语言转换规则的位置从数字服务器类型的转换。 对于这些转换，总是直接截取有效位数（从不四舍五入），而溢出则按目标（较小者）类型取模处理。 例如，在基础调用 updateDecimal **int**包含"1.9999"列将返回"1"，或者，如果基础**十进制**值是"3000000000"则**int**溢出到"-1294967296"的值。  
  
-   **数据相关的 (z)**： 从基础源数据类型为目标数据类型的转换需要可将所含的值转换为目标类型。 不执行其他转换。 如果值对于 getter 类型过大，则该值无效。 例如，如果对包含“53”的 int 列调用 updateString，更新将成功；如果基础字符串值为“foo”或“3000000000”，则将引发错误。  
  
 当上调用 updateString**二进制**， **varbinary**， **varbinary （max)**，或**映像**列的数据类型，它处理的字符串值作为十六进制字符串值。  
  
 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]列数据类型是**XML**，数据值必须为有效**XML**。 调用 updateBytes、 updateBinaryStream 或 updateBlob 方法时，数据值应为十六进制字符串表示形式的 XML 字符。 例如：  
  
```  
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E   
```  
  
 请注意，如果 XML 字符使用特殊的字符编码，则需要字节顺序标记 (BOM)。  
  
## <a name="setter-method-conversions"></a>Setter 方法转换  
 对于 Java 类型化数据传递到第组\<类型 > （） 方法的[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)类和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类，将应用以下转换。  
  
 ![JDBCSetterConversions](../../connect/jdbc/media/jdbc_jdbcsetterconversions_v2.gif "JDBCSetterConversions")  
  
 服务器会尝试所有转换，并在失败时返回错误。  
  
 情况下**字符串**数据类型，如果值超过了**VARCHAR**，它映射到**LONGVARCHAR**。 同样， **NVARCHAR**映射到**LONGNVARCHAR**如果值超过支持的长度的**NVARCHAR**。 同样适用于**byte []**。 值长度超过**VARBINARY**成为**LONGVARBINARY**。  
  
 JDBC Driver 的 setter 方法支持两类转换：  
  
-   **非有损 (x)**： 数值的情况下，setter 类型相同的转换或小于基础的服务器类型。 例如，当在基础的服务器上调用 setBigDecimal**十进制**列，则不必进行转换。 适用于字符的情况，Java**数值**数据类型转换为**字符串**。 例如，调用 varchar(50) 列的值为"53"setDouble 生成该目标列中的字符值"53"。  
  
-   **转换后 (y)**： 从 Java 转换**数值**类型设置为基础服务器**数值**较小的类型。 此转换是正则并遵循[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]转换约定。 总是直接截取有效位数（从不四舍五入），而溢出将引发“不支持的转换”错误。 例如，值为"1.9999"中"1"中的目标列中; 基础整数列结果上使用 updateDecimal但如果传递"3000000000"，该驱动程序将引发错误。  
  
-   **数据相关的 (z)**： 从 Java 转换**字符串**类型设置为基础[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型取决于以下条件： 驱动程序将发送**字符串**的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]执行转换，如有必要。 如果 sendStringParametersAsUnicode 设置为 true，基础[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型是**映像**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]不允许转换**nvarchar**到**映像**并引发 SQLServerException。 如果 sendStringParametersAsUnicode 设置为 false，基础[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型是**映像**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]允许转换**varchar**到**映像**且不引发异常。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 将执行的转换并将错误传递回 JDBC 驱动程序中，有问题时。  
  
 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]列数据类型是**XML**，数据值必须为有效**XML**。 调用 updateBytes、 updateBinaryStream 或 updateBlob 方法时，数据值应为十六进制字符串表示形式的 XML 字符。 例如：  
  
```  
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E   
```  
  
 请注意，如果 XML 字符使用特殊的字符编码，则需要字节顺序标记 (BOM)。  
  
## <a name="conversions-on-setobject"></a>setObject 的转换  
  
> [!NOTE]  
>  Microsoft JDBC Drivers 4.2 （和更高版本） 的 SQL Server 支持 JDBC 4.1 和 4.2。 4.1 和 4.2 数据类型映射和转换的详细信息请参阅[JDBC 驱动程序的 JDBC 4.1 符合性](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md)和[JDBC 驱动程序的 JDBC 4.2 法规遵从性](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)，除了以下信息。  
  
 对于 Java 类型化数据传递给 setObject (\<类型 >) 方法的[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)类，将应用以下转换。  
  
 ![JDBCSetObjectConversions](../../connect/jdbc/media/jdbc_jdbcsetobjectconversions.gif "JDBCSetObjectConversions")  
  
 不带指定的目标类型 setObject 方法使用默认映射。 情况下**字符串**数据类型，如果值超过了**VARCHAR**，它映射到**LONGVARCHAR**。 同样， **NVARCHAR**映射到**LONGNVARCHAR**如果值超过支持的长度的**NVARCHAR**。 同样适用于**byte []**。 值长度超过**VARBINARY**成为**LONGVARBINARY**。  
  
 JDBC Driver 的 setObject 方法支持三类转换：  
  
-   **非有损 (x)**： 数值的情况下，setter 类型相同的转换或小于基础的服务器类型。 例如，当在基础的服务器上调用 setBigDecimal**十进制**列，则不必进行转换。 适用于字符的情况，Java**数值**数据类型转换为**字符串**。 例如，调用 varchar(50) 列的值为"53"setDouble 将生成该目标列中的字符值"53"。  
  
-   **转换后 (y)**： 从 Java 转换**数值**类型设置为基础服务器**数值**较小的类型。 此转换是正则并遵循[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]转换约定。 总是直接截取有效位数（从不四舍五入），而溢出将引发不支持转换的错误。 例如，值为"1.9999"中"1"中的目标列中; 基础整数列结果上使用 updateDecimal但如果传递"3000000000"，该驱动程序将引发错误。  
  
-   **数据相关的 (z)**： 从 Java 转换**字符串**类型设置为基础[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型取决于以下条件： 驱动程序将发送**字符串**的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]执行转换，如有必要。 如果 sendStringParametersAsUnicode 连接属性设置为 true，基础[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型是**映像**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]不允许转换**nvarchar**到**映像**并引发 SQLServerException。 如果 sendStringParametersAsUnicode 设置为 false，基础[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型是**映像**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]允许转换**varchar**到**映像**且不引发异常。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 执行大容量的集转换并将错误传递回 JDBC 驱动程序有问题时。 客户端转换异常，并且仅在的情况下执行**日期**，**时间**，**时间戳**，**布尔**，和**字符串**值。  
  
 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]列数据类型是**XML**，数据值必须为有效**XML**。 调用 setObject(byte[], SQLXML)、setObject(inputStream, SQLXML) 或 setObject(Blob, SQLXML) 方法时，数据值应为 XML 字符的十六进制字符串表示形式。 例如：  
  
```  
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E   
```  
  
 请注意，如果 XML 字符使用特殊的字符编码，则需要字节顺序标记 (BOM)。  
  
## <a name="see-also"></a>另请参阅  
 [了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
