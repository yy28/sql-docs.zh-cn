---
title: Integration Services 数据类型 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- modifying data types
- data types [Integration Services], listed
- data types [Integration Services]
- column data types [Integration Services]
- SSIS, data types
- Integration Services, data types
- SQL Server Integration Services, data types
ms.assetid: 896fc3e8-3aa6-4396-ba82-5d7741cffa56
caps.latest.revision: 98
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: abf3340badf3e1914bce13951625308ac10a3c65
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35407729"
---
# <a name="integration-services-data-types"></a>Integration Services 数据类型
  当数据进入包中的数据流时，提取这些数据的源会将数据转换为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型。 为数值数据分配数值数据类型，为字符串数据分配字符数据类型，为日期分配日期数据类型。 其他数据，如 GUID 和二进制大型对象块 (BLOB)，也要分配相应的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型。 如果数据的数据类型无法转换为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型，则会发生错误。  
  
 某些数据流组件可在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]的托管数据类型之间转换数据类型。 有关 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和托管数据类型之间的映射的详细信息，请参阅 [在数据流中使用数据类型](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)。  
  
 下表列出了 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型。 表中的一些数据类型提供了适用的精度和小数位数信息。 有关精度和小数位数的详细信息，请参阅[精度、小数位数和长度 (Transact-SQL)](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)。  
  
|数据类型|描述|  
|---------------|-----------------|  
|DT_BOOL|一个布尔值。|  
|DT_BYTES|二进制数据值。 长度可变，且最大长度为 8000 字节。|  
|DT_CY|货币值。 此数据类型为八字节有符号整数，其小数位数为 4，最大精度为 19。|  
|DT_DATE|由年、月、日、小时、分钟、秒和小数秒组成的日期结构。  小数秒的固定小数位数为 7。<br /><br /> DT_DATE 数据类型是使用 8 字节浮点数字来实现的。 日以整数增量表示，从 1899 年 12 月 30 日开始，午夜时间为零点。 小时值以数字的小数部分的绝对值表示。 但是，浮点值无法表示所有实数值；因此，可以在 DT_DATE 中显示的日期的范围受到限制。<br /><br /> 另一方面，DT_DBTIMESTAMP 以内部具有单独的年、月、日、小时、分钟、秒和毫秒字段的结构表示。 此数据类型对其能够表示的日期有较大的范围限制。|  
|DT_DBDATE|由年、月和日组成的日期结构。|  
|DT_DBTIME|由小时、分钟和秒组成的时间结构。|  
|DT_DBTIME2|由小时、分钟、秒和小数秒组成的时间结构。 小数秒的最大小数位数为 7。|  
|DT_DBTIMESTAMP|由年、月、日、小时、分钟、秒和小数秒组成的时间戳结构。 小数秒的最大小数位数为 3。|  
|DT_DBTIMESTAMP2|由年、月、日、小时、分钟、秒和小数秒组成的时间戳结构。 小数秒的最大小数位数为 7。|  
|DT_DBTIMESTAMPOFFSET|由年、月、日、小时、分钟、秒和小数秒组成的时间戳结构。 小数秒的最大小数位数为 7。<br /><br /> 与 DT_DBTIMESTAMP 和 DT_DBTIMESTAMP2 数据类型不同，DT_DBTIMESTAMPOFFSET 数据类型具有时区偏移量。 此偏移量指定时间相对于协调世界时 (UTC) 偏移的小时和分钟数。 系统使用时区偏移量获取本地时间。<br /><br /> 时区偏移量必须包括符号（加或减）以表示是用 UTC 加上还是减去偏移量。 偏移量的有效小时数介于 -14 和 +14 之间。 分钟偏移量的符号取决于小时偏移量的符号：<br /><br /> 如果小时偏移量的符号为负，则分钟偏移量必须为负或零。<br /><br /> 如果小时偏移量的符号为正，则分钟偏移量必须为正或零。<br /><br /> 如果小时偏移量的符号为零，则分钟偏移量可以为 -0.59 到 +0.59 之间的任何值。|  
|DT_DECIMAL|精度和小数位数均固定的精确数值。 此数据类型为具有单独符号的十二字节无符号整数，其小数位数为 0 到 28，最大精度为 29。|  
|DT_FILETIME|一个 64 位值，表示从 1601 年 1 月 1 日起长度为 100 纳秒的间隔的数量。 小数秒的最大小数位数为 3。|  
|DT_GUID|全局唯一标识符 (GUID)。|  
|DT_I1|单字节有符号整数。|  
|DT_I2|双字节有符号整数。|  
|DT_I4|四字节有符号整数。|  
|DT_I8|八字节有符号整数。|  
|DT_NUMERIC|精度和小数位数固定的精确数值。 此数据类型为具有单独符号的十六字节无符号整数，其小数位数为 0 到 38，最大精度为 38。|  
|DT_R4|单精度浮点值。|  
|DT_R8|双精度浮点值。|  
|DT_STR|以 null 值结束的 [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]/MBCS 字符串，最大长度为 8000 个字符。 （如果列值包含其他 Null 终止符，则字符串将在第一个 Null 值出现的位置截断。）|  
|DT_UI1|单字节无符号整数。|  
|DT_UI2|双字节无符号整数。|  
|DT_UI4|四字节无符号整数。|  
|DT_UI8|八字节无符号整数。|  
|DT_WSTR|以 Null 值结束的 Unicode 字符串，最大长度为 4000 个字符。 （如果列值包含其他 Null 终止符，则字符串将在第一个 Null 值出现的位置截断。）|  
|DT_IMAGE|二进制值，最大大小为 2^31-1 (2,147,483,647) 个字节。 的托管数据类型之间转换数据类型。|  
|DT_NTEXT|Unicode 字符串，最大长度为 2^30 - 1 (1,073,741,823) 个字符。|  
|DT_TEXT|[!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]/MBCS 字符串，最大长度为 2^31-1 (2,147,483,647) 个字符。|  
  
## <a name="conversion-of-data-types"></a>数据类型的转换  
 如果列中的数据不必是源数据类型分配的全角形式，那么最好更改列的数据类型。 使每个数据行尽可能窄有助于优化传输数据时的性能，因为每行越窄，数据从源移动到目标就越快。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含一组完整的数值数据类型，这样可以使数据类型近似匹配于数据大小。 例如，如果数据类型为 DT_UI8 的列中的值始终为 0 到 3000 之间的整数，则可以将数据类型更改为 DT_UI2。 同样，如果数据类型为 DT_CY 的列改用整数数据类型可以满足包数据要求，则可以将数据类型更改为 DT_I4。  
  
 可以按以下方法更改列的数据类型：  
  
-   使用表达式隐式转换数据类型。 有关详细信息，请参阅[表达式中的 Integration Services 数据类型](../../integration-services/expressions/integration-services-data-types-in-expressions.md)、[表达式中的 Integration Services 数据类型](../../integration-services/expressions/integration-services-data-types-in-expressions.md)和 [Integration Services (SSIS) 表达式](../../integration-services/expressions/integration-services-ssis-expressions.md)。  
  
-   使用转换运算符转换数据类型。 有关详细信息，请参阅[转换（SSIS 表达式）](../../integration-services/expressions/cast-ssis-expression.md)。  
  
-   使用数据转换将列的数据类型从一种数据类型转换为另一种数据类型。 有关详细信息，请参阅 [Data Conversion Transformation](../../integration-services/data-flow/transformations/data-conversion-transformation.md)。  
  
-   使用派生列转换创建数据类型与原始列数据类型不同的列的副本。 有关详细信息，请参阅 [派生列转换](../../integration-services/data-flow/transformations/derived-column-transformation.md)。  
  
### <a name="converting-between-strings-and-datetime-data-types"></a>字符串和日期/时间数据类型之间的转换  
 下表列出了日期/时间数据类型和字符串之间的转换结果：  
  
-   使用转换运算符或数据转换转换时，日期或时间数据类型将转换为相应的字符串格式。 例如，DT_DBTIME 数据类型将转换为格式为“hh:mm:ss”的字符串。  
  
-   要从字符串转换为日期或时间数据类型时，该字符串必须使用与相应的日期或时间数据类型对应的字符串格式。 例如，若要将某些日期字符串成功转换为 DT_DBDATE 数据类型，这些日期字符串的格式必须为“yyyy-mm-dd”。  
  
    |数据类型|字符串格式|  
    |---------------|-------------------|  
    |DT_DBDATE|yyyy-mm-dd|  
    |DT_FILETIME|yyyy-mm-dd hh:mm:ss:fff|  
    |DT_DBTIME|hh:mm:ss|  
    |DT_DBTIME2|hh:mm:ss[.fffffff]|  
    |DT_DBTIMESTAMP|yyyy-mm-dd hh:mm:ss[.fff]|  
    |DT_DBTIMESTAMP2|yyyy-mm-dd hh:mm:ss[.fffffff]|  
    |DT_DBTIMESTAMPOFFSET|yyyy-mm-dd hh:mm:ss[.fffffff] [{+|-} hh:mm]|  
  
 在 DT_FILETIME 和 DT_DBTIMESTAMP 的格式中，fff 是一个表示小数秒的介于 0 和 999 之间的值。  
  
 在 DT_DBTIMESTAMP2、DT_DBTIME2 和 DT_DBTIMESTAMPOFFSET 的日期格式中，fffffff 是一个表示小数秒的介于 0 和 9999999 之间的值。  
  
 DT_DBTIMESTAMPOFFSET 日期格式中还包括一个时区元素。 在时间元素和时区元素之间有一个空格。  
  
### <a name="converting-datetime-data-types"></a>转换日期/时间数据类型  
 可以更改具有日期/时间数据的列的数据类型，以便提取数据的日期或时间部分。 下表列出了将一种日期/时间数据类型更改为另一种日期/时间数据类型的结果。  
  
#### <a name="converting-from-dtfiletime"></a>从 DT_FILETIME 转换  
  
|将 DT_FILETIME 转换为|结果|  
|-----------------------------|------------|  
|DT_FILETIME|没有变化。|  
|DT_DATE|转换该数据类型。|  
|DT_DBDATE|删除时间值。|  
|DT_DBTIME|删除日期值。<br /><br /> 当小数秒值的小数位数超过 DT_DBTIME 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIME2|删除 DT_FILETIME 数据类型表示的日期值。<br /><br /> 当小数秒值的小数位数超过 DT_DBTIME2 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMP|转换该数据类型。|  
|DT_DBTIMESTAMP2|当小数秒值的小数位数超过 DT_DBTIMESTAMP2 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMPOFFSET|将 DT_DBTIMESTAMPOFFSET 数据类型的时区字段设置为零。<br /><br /> 当小数秒值的小数位数超过 DT_DBTIMESTAMPOFFSET 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
  
#### <a name="converting-from-dtdate"></a>从 DT_DATE 转换  
  
|将 DT_DATE 转换为|结果|  
|-------------------------|------------|  
|DT_FILETIME|转换该数据类型。|  
|DT_DATE|没有变化。|  
|DT_DBDATE|删除 DT_DATA 数据类型表示的时间值。|  
|DT_DBTIME|删除 DT_DATE 数据类型表示的日期值。|  
|DT_DBTIME2|删除 DT_DATE 数据类型表示的日期值。|  
|DT_DBTIMESTAMP|转换该数据类型。|  
|DT_DBTIMESTAMP2|转换该数据类型。|  
|DT_DBTIMESTAMPOFFSET|将 DT_DBTIMESTAMPOFFSET 数据类型的时区字段设置为零。|  
  
#### <a name="converting-from-dtdbdate"></a>从 DT_DBDATE 转换  
  
|将 DT_DBDATE 转换为|结果|  
|---------------------------|------------|  
|DT_FILETIME|将 DT_FILETIME 数据类型的时间字段设置为零。|  
|DT_DATE|将 DT_DATE 数据类型的时间字段设置为零。|  
|DT_DBDATE|没有变化。|  
|DT_DBTIME|将 DT_DBTIME 数据类型的时间字段设置为零。|  
|DT_DBTIME2|将 DT_DBTIME2 数据类型的时间字段设置为零。|  
|DT_DBTIMESTAMP|将 DT_DBTIMESTAMP 数据类型的时间字段设置为零。|  
|DT_DBTIMESTAMP2|将 DT_DBTIMESTAMP 数据类型的时间字段设置为零。|  
|DT_DBTIMESTAMPOFFSET|将 DT_DBTIMESTAMPOFFSET 数据类型的时间字段和时区字段设置为零。|  
  
#### <a name="converting-from-dtdbtime"></a>从 DT_DBTIME 转换  
  
|将 DT_DBTIME 转换为|结果|  
|---------------------------|------------|  
|DT_FILETIME|将 DT_FILETIME 数据类型的日期字段设置为当前日期。|  
|DT_DATE|将 DT_DATE 数据类型的日期字段设置为当前日期。|  
|DT_DBDATE|将 DT_DBDATE 数据类型的日期字段设置为当前日期。|  
|DT_DBTIME|没有变化。|  
|DT_DBTIME2|转换该数据类型。|  
|DT_DBTIMESTAMP|将 DT_DBTIMESTAMP 数据类型的日期字段设置为当前日期。|  
|DT_DBTIMESTAMP2|将 DT_DBTIMESTAMP2 数据类型的日期字段设置为当前日期。|  
|DT_DBTIMESTAMPOFFSET|将 DT_DBTIMESTAMPOFFSET 数据类型的日期字段和时区字段分别设置为当前日期和零。|  
  
#### <a name="converting-from-dtdbtime2"></a>从 DT_DBTIME2 转换  
  
|将 DT_DBTIME2 转换为|结果|  
|----------------------------|------------|  
|DT_FILETIME|将 DT_FILETIME 数据类型的日期字段设置为当前日期。<br /><br /> 当小数秒值的小数位数超过 DT_FILETIME 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DATE|将 DT_DATE 数据类型的日期字段设置为当前日期。<br /><br /> 当小数秒值的小数位数超过 DT_DATE 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBDATE|将 DT_DBDATE 数据类型的日期字段设置为当前日期。|  
|DT_DBTIME|当小数秒值的小数位数超过 DT_DBTIME 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIME2|当小数秒值的小数位数超过目标 DT_DBTIME2 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMP|将 DT_DBTIMESTAMP 数据类型的日期字段设置为当前日期。<br /><br /> 当小数秒值的小数位数超过 DT_DBTIMESTAMP 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMP2|将 DT_DBTIMESTAMP2 数据类型的日期字段设置为当前日期。<br /><br /> 当小数秒值的小数位数超过 DT_DBTIMESTAMP2 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMPOFFSET|将 DT_DBTIMESTAMPOFFSET 数据类型的日期字段和时区字段分别设置为当前日期和零。<br /><br /> 当小数秒值的小数位数超过 DT_DBTIMESTAMPOFFSET 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
  
#### <a name="converting-from-dtdbtimestamp"></a>从 DT_DBTIMESTAMP 转换  
  
|将 DT_DBTIMESTAMP 转换为|结果|  
|--------------------------------|------------|  
|DT_FILETIME|转换该数据类型。|  
|DT_DATE|如果 DT_DBTIMESTAMP 数据类型表示的值溢出 DT_DATE 数据类型的范围，则返回 DB_E_DATAOVERFLOW 错误。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBDATE|删除 DT_DBTIMESTAMP 数据类型表示的时间值。|  
|DT_DBTIME|删除 DT_DBTIMESTAMP 数据类型表示的日期值。<br /><br /> 当小数秒值的小数位数超过 DT_DBTIME 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIME2|删除 DT_DBTIMESTAMP 数据类型表示的日期值。<br /><br /> 当小数秒值的小数位数超过 DT_DBTIME2 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMP|没有变化。|  
|DT_DBTIMESTAMP2|当小数秒值的小数位数超过 DT_DBTIMESTAMP2 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMPOFFSET|将 DT_DBTIMESTAMPOFFSET 数据类型的时区字段设置为零。<br /><br /> 当小数秒值的小数位数超过 DT_DBTIMESTAMPOFFSET 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
  
#### <a name="converting-from-dtdbtimestamp2"></a>从 DT_DBTIMESTAMP2 转换  
  
|将 DT_DBTIMESTAMP2 转换为|结果|  
|---------------------------------|------------|  
|DT_FILETIME|当小数秒值的小数位数超过 DT_FILETIME 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DATE|如果 DT_DBTIMESTAMP2 数据类型表示的值溢出 DT_DATE 数据类型的范围，则返回 DB_E_DATAOVERFLOW 错误。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。<br /><br /> 当小数秒值的小数位数超过 DT_DATE 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBDATE|删除 DT_DBTIMESTAMP2 数据类型表示的时间值。|  
|DT_DBTIME|删除 DT_DBTIMESTAMP2 数据类型表示的日期值。<br /><br /> 当小数秒值的小数位数超过 DT_DBTIME 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIME2|删除 DT_DBTIMESTAMP2 数据类型表示的日期值。<br /><br /> 当小数秒值的小数位数超过 DT_DBTIME2 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMP|如果 DT_DBTIMESTAMP2 数据类型表示的值溢出 DT_DBTIMESTAMP 数据类型的范围，则返回 DB_E_DATAOVERFLOW 错误。<br /><br /> DT_DBTIMESTAMP2 映射到 SQL Server 数据类型 datetime2，范围是公元元年 1 月 1 日 到公元 9999 年 12 月 31 日。 DT_DBTIMESTAMP 映射到 SQL Server 数据类型 datetime，具有较小的范围：从 1753 年 1 月 1 日到 9999 年 12 月 31 日。<br /><br /> 当小数秒值的小数位数超过 DT_DBTIMESTAMP 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。<br /><br /> 有关错误的详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMP2|当小数秒值的小数位数超过目标 DT_DBTIMESTAMP2 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMPOFFSET|将 DT_DBTIMESTAMPOFFSET 数据类型的时区字段设置为零。<br /><br /> 当小数秒值的小数位数超过 DT_DBTIMESTAMPOFFSET 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
  
#### <a name="converting-from-dtdbtimestampoffset"></a>从 DT_DBTIMESTAMPOFFSET 转换  
  
|将 DT_DBTIMESTAMPOFFSET 转换为|结果|  
|--------------------------------------|------------|  
|DT_FILETIME|将 DT_DBTIMESTAMPOFFSET 数据类型表示的时间值更改为协调世界时 (UTC)。<br /><br /> 当小数秒值的小数位数超过 DT_FILETIME 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DATE|将 DT_DBTIMESTAMPOFFSET 数据类型表示的时间值更改为 UTC。<br /><br /> 如果 DT_DBTIMESTAMPOFFSET 数据类型表示的值溢出 DT_DATE 数据类型的范围，则返回 DB_E_DATAOVERFLOW 错误。<br /><br /> 当小数秒值的小数位数超过 DT_DATE 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。<br /><br /> 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBDATE|将 DT_DBTIMESTAMPOFFSET 数据类型表示的时间值更改为 UTC，这可能影响日期值。 随后将删除该时间值。|  
|DT_DBTIME|将 DT_DBTIMESTAMPOFFSET 数据类型表示的时间值更改为 UTC。<br /><br /> 删除 DT_DBTIMESTAMPEOFFSET 数据类型表示的数据值。<br /><br /> 当小数秒值的小数位数超过 DT_DBTIME 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIME2|将 DT_DBTIMESTAMPOFFSET 数据类型表示的时间值更改为 UTC。<br /><br /> 删除 DT_DBTIMESTAMPOFFSET 数据类型表示的日期值。<br /><br /> 当小数秒值的小数位数超过 DT_DBTIME2 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMP|将 DT_DBTIMESTAMPOFFSET 数据类型表示的时间值更改为 UTC。<br /><br /> 如果 DT_DBTIMESTAMPOFFSET 数据类型表示的值溢出 DT_DBTIMESTAMP 数据类型的范围，则返回 DB_E_DATAOVERFLOW 错误。<br /><br /> 当小数秒值的小数位数超过 DT_DBTIMESTAMP 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。<br /><br /> 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMP2|将 DT_DBTIMESTAMPOFFSET 数据类型表示的时间值更改为 UTC。<br /><br /> 当小数秒值的小数位数超过 DT_DBTIMESTAMP2 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMPOFFSET|当小数秒值的小数位数超过目标 DT_DBTIMESTAMPOFFSET 数据类型可以包含的小数位数时，删除该小数秒值。 删除小数秒值后，生成有关此数据截断的报告。 有关详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。|  
  
## <a name="mapping-of-integration-services-data-types-to-database-data-types"></a>Integration Services 数据类型到数据库数据类型的映射  
 下表提供了将特定数据库使用的数据类型映射为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型的原则。 这些映射是从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导在从这些源中导入数据时使用的映射文件中汇总而来的。 有关这些映射文件的详细信息，请参阅 [SQL Server 导入和导出向导](~/integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)。  
  
> [!IMPORTANT]  
>  并不是说这些映射表示它们完全等同，而只是提供指导。 在某些情况下，最好使用不同于此表中所示的数据类型。  
  
> [!NOTE]  
>  您可以使用 SQL Server 数据类型来评估相应 Integration Services 日期和时间数据类型的大小。  
  
|数据类型|SQL Server<br /><br /> (SQLOLEDB; SQLNCLI10)|SQL Server (SqlClient)|Jet|Oracle<br /><br /> (OracleClient)|DB2<br /><br /> (DB2OLEDB)|DB2<br /><br /> (IBMDADB2)|  
|---------------|--------------------------------------------|------------------------------|---------|---------------------------------|--------------------------|--------------------------|  
|DT_BOOL|bit|bit|bit||||  
|DT_BYTES|binary、varbinary、timestamp|binary、varbinary、timestamp|BigBinary、VarBinary|RAW|||  
|DT_CY|smallmoney、money|smallmoney、money|货币||||  
|DT_DATE|||||||  
|DT_DBDATE|[date (Transact-SQL)](../../t-sql/data-types/date-transact-sql.md)|[date (Transact-SQL)](../../t-sql/data-types/date-transact-sql.md)||日期|日期|日期|  
|DT_DBTIME||||TIMESTAMP|time|time|  
|DT_DBTIME2|[time (Transact-SQL)](../../t-sql/data-types/time-transact-sql.md) (p)|[time (Transact-SQL)](../../t-sql/data-types/time-transact-sql.md) (p)|||||  
|DT_DBTIMESTAMP|[datetime (Transact-SQL)](../../t-sql/data-types/datetime-transact-sql.md)[smalldatetime (Transact-SQL)](../../t-sql/data-types/smalldatetime-transact-sql.md)|[datetime (Transact-SQL)](../../t-sql/data-types/datetime-transact-sql.md)[smalldatetime (Transact-SQL)](../../t-sql/data-types/smalldatetime-transact-sql.md)|DateTime|TIMESTAMP、DATE、INTERVAL|TIME、TIMESTAMP、DATE|TIME、TIMESTAMP、DATE|  
|DT_DBTIMESTAMP2|[datetime2 (Transact-SQL)](../../t-sql/data-types/datetime2-transact-sql.md)|[datetime2 (Transact-SQL)](../../t-sql/data-types/datetime2-transact-sql.md)||TIMESTAMP|TIMESTAMP|TIMESTAMP|  
|DT_DBTIMESTAMPOFFSET|[datetimeoffset (Transact-SQL)](../../t-sql/data-types/datetimeoffset-transact-sql.md) (p)|[datetimeoffset (Transact-SQL)](../../t-sql/data-types/datetimeoffset-transact-sql.md) (p)||timestampoffset|timestamp,<br /><br /> varchar|timestamp,<br /><br /> varchar|  
|DT_DECIMAL|||||||  
|DT_FILETIME|||||||  
|DT_GUID|UNIQUEIDENTIFIER|UNIQUEIDENTIFIER|GUID||||  
|DT_I1|||||||  
|DT_I2|SMALLINT|SMALLINT|Short||smallint|SMALLINT|  
|DT_I4|ssNoversion|ssNoversion|Long||整数|整数|  
|DT_I8|BIGINT|BIGINT|||BIGINT|bigint|  
|DT_NUMERIC|decimal、numeric|decimal、numeric|Decimal|NUMBER、INT|decimal、numeric|decimal、numeric|  
|DT_R4|REAL|REAL|Single||real|real|  
|DT_R8|float|FLOAT|双精度|FLOAT、REAL|FLOAT、DOUBLE|FLOAT、DOUBLE|  
|DT_STR|char、varchar||varchar||char、varchar|char、varchar|  
|DT_UI1|TINYINT|TINYINT|Byte||||  
|DT_UI2|||||||  
|DT_UI4|||||||  
|DT_UI8|||||||  
|DT_WSTR|nchar、nvarchar、sql_variant、xml|char、varchar、nchar、nvarchar、sql_variant、xml|LongText|CHAR、ROWID、VARCHAR2、NVARCHAR2、NCHAR|GRAPHIC、VARGRAPHIC|GRAPHIC、VARGRAPHIC|  
|DT_IMAGE|图像|图像|LongBinary|LONG RAW、BLOB、LOBLOCATOR、BFILE、VARGRAPHIC、LONG VARGRAPHIC、用户定义|CHAR () FOR BIT DATA、VARCHAR () FOR BIT DATA|CHAR () FOR BIT DATA、VARCHAR () FOR BIT DATA、BLOB|  
|DT_NTEXT|ntext|text、ntext||LONG、CLOB、NCLOB、NVARCHAR、TEXT|LONG VARCHAR、NCHAR、NVARCHAR、TEXT|LONG VARCHAR、DBCLOB、NCHAR、NVARCHAR、TEXT|  
|DT_TEXT|text||||LONG VARCHAR FOR BIT DATA|LONG VARCHAR FOR BIT DATA、CLOB|  
  
 有关在数据流中映射数据类型的信息，请参阅 [在数据流中使用数据类型](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)。  
  
## <a name="related-content"></a>相关内容  
 blogs.msdn.com 上的博客文章 [SSIS 2008 中数据类型转换技术之间的性能比较](http://go.microsoft.com/fwlink/?LinkId=220823)。  
  
## <a name="see-also"></a>另请参阅  
 [数据流中的数据](../../integration-services/data-flow/data-in-data-flows.md)  
  
  
