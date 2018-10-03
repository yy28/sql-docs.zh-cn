---
title: 了解数据类型的差异 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab8fa00f-cb16-47e2-94b8-3a76f56c2b84
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 546dc71fad06fc69d816d16c1d6c2d67f59f968b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773200"
---
# <a name="understanding-data-type-differences"></a>了解数据类型的差异

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Java 编程语言数据类型和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型之间存在很多差异。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 通过各种类型的转换来帮助消除这些差异。  

## <a name="character-types"></a>字符类型

JDBC 字符串数据类型为**CHAR**， **VARCHAR**，并**LONGVARCHAR**。 JDBC 提供程序提供对 JDBC 4.0 API 的支持。 在 JDBC 4.0 中，JDBC 字符串数据类型也可以是**NCHAR**， **NVARCHAR**，并**LONGNVARCHAR**。 这些新的字符串类型以 Unicode 格式维护 Java 本机字符类型，从而不必执行任何 ANSI 到 Unicode 或 Unicode 到 ANSI 的转换。  
  
| 类型            | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 固定长度    | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Char**并**nchar**数据类型直接映射到 JDBC **CHAR**并**NCHAR**类型。 这些都是在列具有 `SET ANSI_PADDING ON` 的情况下，带有由服务器提供的填充的固定长度的类型。 对于 nchar，填充始终是启用的，但对于 char，在未填充服务器字符列的情况下，JDBC 驱动程序将添加填充。                                                                                                                                                                                                                                                                                                                                                                                      |
| Variable-length | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Varchar**并**nvarchar**类型直接映射到 JDBC **VARCHAR**并**NVARCHAR**分别类型。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Long            | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **文本**并**ntext**类型映射到 JDBC **LONGVARCHAR**并**LONGNVARCHAR**分别键入。 这些是不推荐使用的类型从[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，因此应改用大值类型**varchar （max)** 或**nvarchar （max)**，改为。<br /><br /> 使用更新\<数值类型 > 和[updateObject （int，java.lang.Object）](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md)方法将针对失败**文本**并**ntext** server 列。 然而，对于 text 和 ntext 服务器列，支持将 [setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) 方法用于指定的字符转换类型。 |
  
## <a name="binary-string-types"></a>二进制字符串类型

JDBC 二进制字符串类型为**二进制**， **VARBINARY**，并**LONGVARBINARY**。  
  
| 类型            | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 固定长度    | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **二进制**类型直接映射到 JDBC**二进制**类型。 这是在列具有 SET ANSI_PADDING ON 的情况下，具有由服务器提供填充的固定长度类型。 没有填充服务器 char 列时，JDBC 驱动程序会添加填充。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **时间戳**类型是 JDBC**二进制**具有 8 个字节的固定长度类型。 |
| Variable-length | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Varbinary**类型映射到 JDBC **VARBINARY**类型。<br /><br /> **Udt**中键入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]映射到 JDBC 作为**VARBINARY**类型。                                                                                                                                                                                                                                 |
| Long            | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **映像**类型映射到 JDBC **LONGVARBINARY**类型。 从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 开始不推荐使用此类型，因此应改用大值类型 varbinary(max)。                                                                                                                                                                                           |
  
## <a name="exact-numeric-types"></a>精确数字类型

JDBC 精确数字类型直接映射到其对应的 SQL Server 类型。  
  
| 类型     | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BIT      | JDBC BIT 类型表示单个位（可能为 0 或 1）。 这将映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**位**类型。                                                                                                                                                                                                                                                                                                                                       |
| TINYINT  | JDBC TINYINT 类型表示单个字节。 这将映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **tinyint**类型。                                                                                                                                                                                                                                                                                                                                                 |
| SMALLINT | JDBC SMALLINT 类型表示有符号的 16 位整数。 这将映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **smallint**类型。                                                                                                                                                                                                                                                                                                                                     |
| 整数  | JDBC INTEGER 类型表示有符号的 32 位整数。 这将映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **int**类型。                                                                                                                                                                                                                                                                                                                                           |
| bigint   | JDBC BIGINT 类型表示有符号的 64 位整数。 这将映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bigint**类型。                                                                                                                                                                                                                                                                                                                                         |
| NUMERIC  | JDBC NUMERIC 类型表示固定精度的十进制值，它可存放相同精度的值。 **数值**类型映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**数值**类型。                                                                                                                                                                                                                                                                   |
| DECIMAL  | JDBC DECIMAL 类型表示固定精度的十进制值，它可存放至少具有指定精度的值。 **十进制**类型映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**十进制**类型。<br /><br /> JDBC DECIMAL 类型还映射到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] money 和 smallmoney 类型，这些类型是特定的固定精度的十进制类型，分别以 8 个字节和 4 个字节进行存储。 |
  
## <a name="approximate-numeric-types"></a>近似数字类型

JDBC 近似数值类型包括**真实**， **DOUBLE**，并**FLOAT**。  
  
| 类型   | 描述                                                                                                                                                                                                                                                                                                   |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| real   | JDBC REAL 类型具有 7 位精度（单精度）并直接映射到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]real 类型。                                                                                                                                     |
| DOUBLE | JDBC DOUBLE 类型具有 15 位精度（双精度）并映射到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] float 类型。 JDBC**浮动**类型是的同义词**DOUBLE**。 因为可以有之间产生混淆**FLOAT**并**DOUBLE**， **DOUBLE**是首选。 |
  
## <a name="datetime-types"></a>日期时间类型

JDBC**时间戳**类型映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime**并**smalldatetime**类型。 datetime 类型以两个 4 字节整数进行存储。 smalldatetime 类型可存放相同的信息（日期和时间），但精度较低，为两个 2 字节的小整数。  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] timestamp 类型是固定长度的二进制字符串类型。 它不映射到任何 JDBC 时间类型：**日期**，**时间**，或**时间戳**。  
  
## <a name="custom-type-mapping"></a>自定义类型映射

JDBC 驱动程序中未实现将 SQLData 接口用于 JDBC 高级类型（UDT、Struct 等） JDBC 驱动程序中尚未实现。  
  
## <a name="see-also"></a>另请参阅

[了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
