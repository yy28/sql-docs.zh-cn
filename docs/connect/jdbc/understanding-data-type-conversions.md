---
title: 了解数据类型转换 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 98fa7488-aac3-45b4-8aa4-83ed6ab638b4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5ed91f1b38f68715cd174a96cb2f0364fc060482
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027486"
---
# <a name="understanding-data-type-conversions"></a>了解数据类型转换

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

为了简化 Java 编程语言数据类型到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型的转换，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 根据 JDBC 规范的要求提供了数据类型转换。 为了增加灵活性, 所有类型都可以与**Object**、 **String**和**byte []** 数据类型相互转换。

## <a name="getter-method-conversions"></a>Getter 方法转换

根据 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型，以下图表包含 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 类的 get\<Type>() 方法的 JDBC 驱动程序转换映射，以及 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 类的 get\<Type> 方法的受支持转换。

![JDBCGetterConversions](../../connect/jdbc/media/jdbcgetterconversions.gif "JDBCGetterConversions")

JDBC 驱动程序的 getter 方法支持三类转换：

- **非丢失 (x)** ：适用于 getter 类型与基础服务器类型相同或者小于基础服务器类型时的转换。 例如，对基础服务器十进制数列调用 getBigDecimal 时，无需进行转换。

- **已转换 (y)** ：从数值服务器类型转换为 Java 语言类型，其中转换是常规的并遵循 Java 语言转换规则。 对于这些转换，总是直接截取有效位数（从不四舍五入），而溢出则按目标类型取模处理，以较小者为准。 例如, 对包含 "1.9999" 的基础**十进制**列调用 getInt 将返回 "1"; 如果基础**十进制**值为 "3000000000", 则**int**值将溢出为 "-1294967296"。

- **依赖于数据 (z)** ：如果从基础字符类型转换到数值类型，则要求字符类型包含可转换为该数值类型的值。 不执行其他转换。 如果值对于 getter 类型过大，则该值无效。 例如，如果对包含“53”的 varchar(50) 列调用 getInt，则值将作为 int 返回；如果基础值为“xyz”或“3000000000”，则将引发错误  。

如果对**binary**、 **varbinary**、 **varbinary (max)** 或**image**列数据类型调用 getString, 则值将作为十六进制字符串值返回。

## <a name="updater-method-conversions"></a>Updater 方法转换

对于传递给 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 类的 update\<Type>() 方法的 Java 类型的数据，可应用下列转换。

![JDBCUpdaterConversions](../../connect/jdbc/media/jdbc_jdbcupdatterconversions.gif "JDBCUpdaterConversions")

JDBC 驱动程序的 updater 方法支持三类转换：

- **非丢失 (x)** ：适用于 updater 类型与基础服务器类型相同或者小于基础服务器类型时的转换。 例如，对基础服务器十进制数列调用 updateBigDecimal 时，无需进行转换。

- **已转换 (y)** ：从数值服务器类型转换为 Java 语言类型，其中转换是常规的并遵循 Java 语言转换规则。 对于这些转换，总是直接截取有效位数（从不四舍五入），而溢出则按目标（较小者）类型取模处理。 例如, 对包含 "1.9999" 的基础**int**列调用 updateDecimal 将返回 "1"; 如果基础**十进制**值为 "3000000000", 则**int**值将溢出为 "-1294967296"。

- **依赖于数据 (z)** ：如果从基础源数据类型转换到目标数据类型，则要求源数据类型包含可转换为目标数据类型的值。 不执行其他转换。 如果值对于 getter 类型过大，则该值无效。 例如，如果对包含“53”的 int 列调用 updateString，更新将成功；如果基础字符串值为“foo”或“3000000000”，则将引发错误。

当对**binary**、 **varbinary**、 **varbinary (max)** 或**image**列数据类型调用 updateString 时, 它会将字符串值作为十六进制字符串值进行处理。

当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列的数据类型为 XML 时，数据值必须是有效的 XML   。 调用 updateBytes、updateBinaryStream 或 updateBlob 方法时, 数据值应为 XML 字符的十六进制字符串表示形式。 例如：

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

请注意，如果 XML 字符使用特殊的字符编码，则需要字节顺序标记 (BOM)。

## <a name="setter-method-conversions"></a>Setter 方法转换

对于传递给 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 类和 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 类的 set\<Type>() 方法的 Java 类型的数据，可应用下列转换。

![JDBCSetterConversions](../../connect/jdbc/media/jdbc_jdbcsetterconversions_v2.gif "JDBCSetterConversions")

服务器会尝试所有转换，并在失败时返回错误。

对于**字符串**数据类型, 如果值超过**VARCHAR**的长度, 它将映射到**LONGVARCHAR**。 同样, 如果值超过了支持的**nvarchar**长度, 则**NVARCHAR**映射到**LONGNVARCHAR** 。 这同样适用于 byte[]  。 比**VARBINARY**更长的值会变为**LONGVARBINARY**。

JDBC 驱动程序的 setter 方法支持两类转换：

- **非丢失 (x)** ：适用于 setter 类型与基础服务器类型相同或者小于基础服务器类型时的数值转换。 例如，对基础服务器十进制数列调用 setBigDecimal 时，无需进行转换  。 对于数值转换为字符的情形，Java numeric 数据类型转换为 String   。 例如，使用值“53”对 varchar(50) 列调用 setDouble 时将在该目标列中生成字符值“53”。

- **已转换 (y)** ：从 Java numeric 类型转换为更小的基础服务器 numeric 类型   。 该转换为常规转换，并且遵循 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 转换约定。 总是直接截取有效位数（从不四舍五入），而溢出将引发“不支持的转换”错误。 例如，通过值“1.9999”对基础整数列使用 updateDecimal 时，将在目标列中生成“1”；但如果传递的值为“3000000000”，驱动程序将引发错误。

- **依赖于数据 (z)** ：从 Java String 类型转换到基础 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型取决于以下条件：如有必要，驱动程序会将字符串值发送给 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 再执行转换   。 如果 sendStringParametersAsUnicode 设置为 True，并且基础 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型为 image  ，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将不允许将 nvarchar  转换为 image  并会引发 SQLServerException。 如果 sendStringParametersAsUnicode 设置为 False，并且基础 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型为 image，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将允许将 varchar 转换为 image，而不会引发异常    。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 执行转换，并在出现问题时将错误传回 JDBC 驱动程序。

当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列的数据类型为 XML 时，数据值必须是有效的 XML   。 调用 updateBytes、updateBinaryStream 或 updateBlob 方法时, 数据值应为 XML 字符的十六进制字符串表示形式。 例如：

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

请注意，如果 XML 字符使用特殊的字符编码，则需要字节顺序标记 (BOM)。

## <a name="conversions-on-setobject"></a>setObject 的转换

> [!NOTE]  
> 适用于 SQL Server 的 Microsoft JDBC 驱动程序 4.2 (及更高版本) 支持 JDBC 4.1 和4.2。 有关4.1 和4.2 数据类型映射和转换的更多详细信息, 请参阅 jdbc 驱动程序[的 jdbc 4.1 符合性](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md)和[jdbc 驱动程序的 jdbc 4.2 符合](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)性, 以及以下信息。

对于传递给 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 类的 setObject(\<Type>) 方法的 Java 类型的数据，可应用下列转换。

![JDBCSetObjectConversions](../../connect/jdbc/media/jdbc_jdbcsetobjectconversions.gif "JDBCSetObjectConversions")

没有指定目标类型的 setObject 方法将使用默认映射。 对于**字符串**数据类型, 如果值超过**VARCHAR**的长度, 它将映射到**LONGVARCHAR**。 同样, 如果值超过了支持的**nvarchar**长度, 则**NVARCHAR**映射到**LONGNVARCHAR** 。 这同样适用于 byte[]  。 比**VARBINARY**更长的值会变为**LONGVARBINARY**。

JDBC 驱动程序的 setObject 方法支持三类转换：

- **非丢失 (x)** ：适用于 setter 类型与基础服务器类型相同或者小于基础服务器类型时的数值转换。 例如，对基础服务器十进制数列调用 setBigDecimal 时，无需进行转换  。 对于数值转换为字符的情形，Java numeric 数据类型转换为 String   。 例如，使用值“53”对 varchar(50) 列调用 setDouble 时将在该目标列中生成字符值“53”。

- **已转换 (y)** ：从 Java numeric 类型转换为更小的基础服务器 numeric 类型   。 该转换为常规转换，并且遵循 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 转换约定。 总是直接截取有效位数（从不四舍五入），而溢出则会抛出“转换不受支持”错误。 例如，通过值“1.9999”对基础整数列使用 updateDecimal 时，将在目标列中生成“1”；但如果传递的值为“3000000000”，驱动程序将引发错误。

- **依赖于数据 (z)** ：从 Java String 类型转换到基础 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型取决于以下条件：如有必要，驱动程序会将字符串值发送给 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 再执行转换   。 如果 sendStringParametersAsUnicode 连接属性设置为 True，并且基础 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型为 image，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将不允许将 nvarchar 转换为 image 并会引发 SQLServerException    。 如果 sendStringParametersAsUnicode 设置为 False，并且基础 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型为 image，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将允许将 varchar 转换为 image，而不会引发异常    。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 执行大部分设置转换，并且在出现问题时将错误传回 JDBC 驱动程序。 客户端转换是例外情况, 仅在**日期**、**时间**、时间**戳**、**布尔**值和**字符串**值的情况下执行。

当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列的数据类型为 XML 时，数据值必须是有效的 XML   。 调用 setObject(byte[], SQLXML)、setObject(inputStream, SQLXML) 或 setObject(Blob, SQLXML) 方法时，数据值应为 XML 字符的十六进制字符串表示形式。 例如：

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

请注意，如果 XML 字符使用特殊的字符编码，则需要字节顺序标记 (BOM)。

## <a name="see-also"></a>另请参阅

[了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)
