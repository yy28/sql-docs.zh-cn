---
title: 数据类型使用情况 |微软文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0384857c53e898af9fca89bb2ee2351f0b65f986
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297850"
---
# <a name="data-type-usage"></a>数据类型用法
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 ODBC 驱动程序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，并强制使用以下数据类型。  
  
|数据类型|限制|  
|---------------|----------------|  
|日期文字|日期文本，当存储在SQL_TYPE_TIMESTAMP列（[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**日期时间**或**小日期时间的**数据类型）时，时间值为上午 12：00：00.000。|  
|**钱****和小钱**|只有**货币**和小**货币**数据类型的整数部分才显著。 如果在数据类型转换期间截断 SQL**货币**数据的十进制部分，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序将返回警告，而不是错误。|  
|SQL_BINARY（可以为 Null）|连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 版和更早版本的实例时，如果 SQL_BINARY 列可以为 Null，则在数据源中存储的数据不使用零进行填充。 检索此类列中的数据时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序将右侧的零填充。 但是，在由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 执行的操作（比如串联）中所创建的数据则没有这样的填充。<br /><br /> 而且，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 或更早版本的实例中将数据放在这样的列中时，如果数据太长而无法放入列中，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将截断右侧数据。<br /><br /> 注意：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序确实支持连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 和更早版本。|  
|SQL_CHAR（截断）|在连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 和更早版本的实例并将数据放入 SQL_CHAR 列中时，如果数据太长而无法放入该列中，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将在没有警告的情况下从右侧截断它。<br /><br /> 注意：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序确实支持连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 和更早版本。|  
|SQL_CHAR（可以为 Null）|连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 和更早版本的实例时，如果 SQL_CHAR 列可以为 Null，则不以空白填充数据源中存储的数据。 检索此类列中的数据时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序会用右侧的空白填充数据。 但是，在由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 执行的操作（比如串联）中所创建的数据则没有这样的填充。<br /><br /> 注意：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序确实支持连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 和更早版本。|  
|SQL_LONGVARBINARY、SQL_LONGVARCHAR、SQL_WLONGVARCHAR|连接到 6 的实例时，完全支持使用SQL_LONGVARBINARY、SQL_LONGVARCHAR或SQL_WLONGVARCHAR数据类型（使用 WHERE 子句）影响多个行的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]列的更新。*x*及更高版本。 当连接到实例 4.2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *x*时，S1000 错误"部分插入/更新"。 文本或图像列的插入/更新失败”。<br /><br /> 注意：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序确实支持连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 和更早版本。|  
|字符串函数参数|*字符串函数的string_exp*参数必须是数据类型SQL_CHAR或SQL_VARCHAR。 在字符串函数中不支持 SQL_LONG_VARCHAR 数据类型。 *计数*参数必须小于或等于 8，000，因为SQL_CHAR和SQL_VARCHAR数据类型限制为 8，000 个字符的最大长度。|  
|时间文字|时间文本，当存储在SQL_TIMESTAMP列（[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**日期时间**或**小日期时间的**数据类型）的日期值为 1900 年 1 月 1 日。|  
|**时间 戳**|只能手动将 NULL 值插入**时间戳**列。 但是，由于**时间戳**列由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]自动更新，因此将覆盖 NULL 值。|  
|**小金特**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**小字体**数据类型是无符号的。 默认情况下 **，小列**绑定到数据类型的变量SQL_C_UTINYINT。|  
|别名数据类型|当连接到 4.2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *x*的实例时，ODBC 驱动程序将 NULL 添加到不显式声明列的 null 的列定义。 因此，将忽略在别名数据类型的定义中存储的为 Null 性。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]当连接到 4.2*x*的实例时，具有别名数据类型的列具有**字符**或**二进制**的基本数据类型，并且不声明 null，则创建为数据类型**varchar**或**varbinary**。 [SQLColAttribute、SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)和[SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)[SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md)返回SQL_VARCHAR或SQL_VARBINARY作为这些列的数据类型。 不对从这些列检索的数据进行填充。<br /><br /> 注意：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序确实支持连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 和更早版本。|  
|LONG 数据类型|*对于*SQL_LONGVARBINARY和SQL_LONGVARCHAR数据类型，执行时的数据参数都受到限制。|  
|大值类型|本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 ODBC 驱动程序将在接受或返回 ODBC SQL 数据类型的 API 中公开**varchar（最大值****）、varbinary（max）** 和**nvarchar（max）** 类型，作为 SQL_VARCHAR、SQL_VARBINARY和SQL_WVARCHAR（分别为）。|  
|用户定义类型 （UDT）|UDT 列被映射为 SQL_SS_UDT。 如果使用 UDT 的 ToString() 或 ToXMLString() 方法或者通过 CAST/CONVERT 函数，在 SQL 语句中将 UDT 列显式映射到另一种类型，则在结果集中该列的类型将反映该列被转换成的实际类型。<br /><br /> 本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 ODBC 驱动程序只能绑定到 UDT 列作为二进制。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 仅支持在 SQL_SS_UDT 和 SQL_C_BINARY 数据类型之间的转换。|  
|XML|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会自动将 XML 转换为 Unicode 文本。 XML 类型将映射为 SQL_SS_XML。|  
  
## <a name="see-also"></a>另请参阅  
 [处理结果&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
