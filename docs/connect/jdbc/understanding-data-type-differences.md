---
title: 了解数据类型的区别 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ab8fa00f-cb16-47e2-94b8-3a76f56c2b84
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5395b915d2f261813495d364730d0442a8139334
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="understanding-data-type-differences"></a>了解数据类型的差异
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  有大量的 Java 编程语言的数据类型之间的差异和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]有助于促进通过各种类型的转换这些差异。  
  
## <a name="character-types"></a>字符类型  
 JDBC 字符字符串数据类型都是**CHAR**， **VARCHAR**，和**LONGVARCHAR**。 JDBC 提供程序提供对 JDBC 4.0 API 的支持。 JDBC 4.0 中 JDBC 字符字符串数据类型也可以是**NCHAR**， **NVARCHAR**，和**LONGNVARCHAR**。 这些新的字符串类型以 Unicode 格式维护 Java 本机字符类型，从而不必执行任何 ANSI 到 Unicode 或 Unicode 到 ANSI 的转换。  
  
|类型|Description|  
|----------|-----------------|  
|固定长度|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Char**和**nchar**数据类型映射到 JDBC 直接**CHAR**和**NCHAR**类型。 这些都是在列具有 SET ANSI_PADDING ON 的情况下，具有由服务器提供的填充的固定长度的类型。 填充始终开启的**nchar**，但对于**char**，其中不填充 server char 列的情况下，在 JDBC 驱动程序添加填充。|  
|Variable-length|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Varchar**和**nvarchar**类型直接映射到 JDBC **VARCHAR**和**NVARCHAR**分别类型。|  
|Long|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**文本**和**ntext**类型映射到 JDBC **LONGVARCHAR**和**LONGNVARCHAR**分别键入。 这些是不推荐使用的类型从[!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]，因此你应使用较大的值类型**varchar （max)** 或**nvarchar (max)**，而不是。<br /><br /> 使用更新\<数值类型 > 和[updateObject （int、 java.lang.Object）](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md)方法将会失败针对**文本**和**ntext** server 列。 但是，使用[setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)对于支持与指定的字符转换类型的方法**文本**和**ntext** server 列。|  
  
## <a name="binary-string-types"></a>二进制字符串类型  
 JDBC 二进制字符串类型**二进制**， **VARBINARY**，和**LONGVARBINARY**。  
  
|类型|Description|  
|----------|-----------------|  
|固定长度|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**二进制**类型映射到 JDBC 直接**二进制**类型。 这是在列具有 SET ANSI_PADDING ON 的情况下，具有由服务器提供填充的固定长度类型。 没有填充服务器 char 列时，JDBC 驱动程序会添加填充。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**时间戳**类型是 JDBC**二进制**固定长度为 8 个字节的类型。|  
|Variable-length|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Varbinary**类型映射到 JDBC **VARBINARY**类型。<br /><br /> **Udt**键入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]映射到为 JDBC **VARBINARY**类型。|  
|Long|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**映像**类型映射到 JDBC **LONGVARBINARY**类型。 在从开始已弃用此类型[!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]，因此你应使用大值类型， **varbinary （max)** 相反。|  
  
## <a name="exact-numeric-types"></a>精确数字类型  
 JDBC 精确数字类型直接映射到其对应的 SQL Server 类型。  
  
|类型|Description|  
|----------|-----------------|  
|BIT|JDBC**位**类型表示可以为 0 或 1 中的一个位。 此方法映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**位**类型。|  
|TINYINT|JDBC **TINYINT**类型表示单个字节。 此方法映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **tinyint**类型。|  
|SMALLINT|JDBC **SMALLINT**类型表示 16 位有符号的整数。 此方法映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **smallint**类型。|  
|整数|JDBC**整数**类型表示一个带符号的 32 位整数。 此方法映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **int**类型。|  
|bigint|JDBC **BIGINT**类型表示一个带符号的 64 位整数。 此方法映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **bigint**类型。|  
|NUMERIC|JDBC**数值**类型表示一个固定精度的十进制值，保留相同的精度值。 **数值**类型映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**数值**类型。|  
|DECIMAL|JDBC**十进制**类型表示的至少保留值指定精度的固定精度十进制值。 **十进制**类型映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**十进制**类型。<br /><br /> JDBC**十进制**类型也映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **money**和**smallmoney**类型，它们是 8 和 4 中存储的特定固定精度十进制类型字节，分别。|  
  
## <a name="approximate-numeric-types"></a>近似数字类型  
 JDBC 近似数值类型有**实际**， **DOUBLE**，和**FLOAT**。  
  
|类型|Description|  
|----------|-----------------|  
|REAL|JDBC**实际**类型有七位精度 （单精度） 和直接映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**实际**类型。|  
|DOUBLE|JDBC **DOUBLE**类型有 15 位精度 （双精度），并将映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **float**类型。 JDBC **FLOAT**类型是同义词的**DOUBLE**。 因为可能存在之间产生混淆**FLOAT**和**DOUBLE**， **DOUBLE**是首选。|  
  
## <a name="datetime-types"></a>日期时间类型  
 JDBC**时间戳**类型映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **datetime**和**smalldatetime**类型。 **Datetime**类型存储在两个 4 字节整数。 **Smalldatetime**类型包含的相同信息 （日期和时间），但具有更少的准确性，在两个 2 字节小整数。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**时间戳**类型是固定长度的二进制文件字符串类型。 未映射到任何 JDBC 时间类型：**日期**，**时间**，或**时间戳**。  
  
## <a name="custom-type-mapping"></a>自定义类型映射  
 用于 JDBC 的 sql 数据接口的 JDBC 的自定义类型映射功能的高级类型 （Udt、 结构等）。 不在的 JDBC 驱动程序中实现。  
  
## <a name="see-also"></a>另请参阅  
 [了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
