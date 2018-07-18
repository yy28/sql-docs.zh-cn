---
title: 数据类型使用情况 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC data types
- ODBC data types, about ODBC data types
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC]
- SQL Server Native Client ODBC driver, data types
- data types [ODBC], about data types
ms.assetid: 4f19b0d6-94ac-4a98-a121-57d38787864c
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 56882c7ee5cc588a67d0828ba4d267903be00544
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413166"
---
# <a name="data-type-usage"></a>数据类型用法
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]施加以下使用数据类型。  
  
|数据类型|限制|  
|---------------|----------------|  
|日期文字|日期文字存储在 SQL_TYPE_TIMESTAMP 列 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的数据类型**datetime**或**smalldatetime**)，具有 12:00:00.000 A.M.的时间值|  
|**money**和**smallmoney**|仅整数部分**资金**并**smallmoney**数据类型有意义。 如果 SQL 的小数部分**资金**数据类型在转换期间，数据将被截断[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序将返回警告而不是错误。|  
|SQL_BINARY（可以为 Null）|连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 版和更早版本的实例时，如果 SQL_BINARY 列可以为 Null，则在数据源中存储的数据不使用零进行填充。 当检索来自这样的列的数据时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序以在右侧的零进行填充。 但是，在由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 执行的操作（比如串联）中所创建的数据则没有这样的填充。<br /><br /> 而且，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 或更早版本的实例中将数据放在这样的列中时，如果数据太长而无法放入列中，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将截断右侧数据。<br /><br /> 注意： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 和更早版本。|  
|SQL_CHAR（截断）|在连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 和更早版本的实例并将数据放入 SQL_CHAR 列中时，如果数据太长而无法放入该列中，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将在没有警告的情况下从右侧截断它。<br /><br /> 注意： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 和更早版本。|  
|SQL_CHAR（可以为 Null）|连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 和更早版本的实例时，如果 SQL_CHAR 列可以为 Null，则不以空白填充数据源中存储的数据。 当检索来自这样的列的数据时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序来填充它以在右侧的空白。 但是，在由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 执行的操作（比如串联）中所创建的数据则没有这样的填充。<br /><br /> 注意： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 和更早版本。|  
|SQL_LONGVARBINARY、SQL_LONGVARCHAR、SQL_WLONGVARCHAR|连接到的实例时，完全支持具有 SQL_LONGVARBINARY、 SQL_LONGVARCHAR 或 SQL_WLONGVARCHAR 数据类型 （使用 WHERE 子句） 影响多个行的列的更新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6。*x*及更高版本。 连接到的实例时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]4.2*x*，返回 S1000 错误、"部分插入/更新。 文本或图像列的插入/更新失败”。<br /><br /> 注意： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 和更早版本。|  
|字符串函数参数|*string_exp* SQL_CHAR 或 SQL_VARCHAR 类型到字符串的数据必须是函数的参数。 在字符串函数中不支持 SQL_LONG_VARCHAR 数据类型。 *计数*因为 SQL_CHAR 和 SQL_VARCHAR 数据类型不限制为 8,000 个字符的最大长度参数必须小于或等于 8,000。|  
|时间文字|时间文字存储在 SQL_TIMESTAMP 列 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的数据类型**datetime**或**smalldatetime**)，1900 年 1 月 1 日的日期值。|  
|**timestamp**|可以手动插入 NULL 值**时间戳**列。 但是，由于**时间戳**列将自动更新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，NULL 值会被覆盖。|  
|**tinyint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Tinyint**数据类型是无符号。 一个**tinyint**列将绑定到数据类型为 SQL_C_UTINYINT 的变量，默认情况下。|  
|别名数据类型|连接到的实例时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]4.2*x*，ODBC 驱动程序未显式声明列的为 null 性的列定义中添加 NULL。 因此，将忽略在别名数据类型的定义中存储的为 Null 性。<br /><br /> 连接到的实例时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]4.2*x*，具有基础数据的别名数据类型的列的类型**char**或**二进制**并不为 null 性为声明创建的数据类型为**varchar**或**varbinary**。 [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)， [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)，和[SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md)返回 SQL_VARCHAR 或 SQL_VARBINARY 作为数据类型为这些列。 不对从这些列检索的数据进行填充。<br /><br /> 注意： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 和更早版本。|  
|LONG 数据类型|*执行时数据*参数都被限制为 SQL_LONGVARBINARY 和 SQL_LONGVARCHAR 数据类型。|  
|大值类型|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序将公开**varchar （max)**， **varbinary （max)**，并且**nvarchar （max)** 为 SQL_VARCHAR、 SQL_VARBINARY 和 SQL_ 类型WVARCHAR （分别） 的 Api，接受或返回 ODBC SQL 数据类型。|  
|用户定义类型 (UDT)|UDT 列被映射为 SQL_SS_UDT。 如果使用 UDT 的 ToString() 或 ToXMLString() 方法或者通过 CAST/CONVERT 函数，在 SQL 语句中将 UDT 列显式映射到另一种类型，则在结果集中该列的类型将反映该列被转换成的实际类型。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序只能绑定到 UDT 列作为二进制文件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 仅支持在 SQL_SS_UDT 和 SQL_C_BINARY 数据类型之间的转换。|  
|XML|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会自动将 XML 转换为 Unicode 文本。 XML 类型将映射为 SQL_SS_XML。|  
  
## <a name="see-also"></a>请参阅  
 [处理结果&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
