---
title: 转换执行从服务器到客户端 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB], server to client
ms.assetid: 676fdf24-fb72-4ea0-a8d2-2b197da3c83f
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: f6af4153b94a5c7733b0c91dc31d5a5323642879
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39542057"
---
# <a name="conversions-performed-from-server-to-client"></a>在服务器和客户端之间执行的转换
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  本主题说明在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更高版本）与使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 编写的客户端应用程序之间执行的日期/时间转换。  
  
## <a name="conversions"></a>转换  
 下表说明了返回到客户端的类型与绑定中的类型之间的转换。 对于输出参数，如果在调用 icommandwithparameters:: Setparameterinfo 和中指定的类型*pwszDataSourceType*不的匹配将由服务器执行在服务器上，隐式转换的实际类型并返回到客户端的类型将匹配 icommandwithparameters:: Setparameterinfo 通过指定的类型。 如果服务器的转换规则与本主题中介绍的规则不同，则可能会导致意外的转换结果。 例如，在必须提供默认日期时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 1900-1-1，而不是 1899-12-30。  
  
|目标 -><br /><br /> From|DATE|DBDATE|DBTIME|DBTIME2|DBTIMESTAMP|DBTIMESTAMPOFFSET|FILETIME|BYTES|VARIANT|SSVARIANT|BSTR|STR|WSTR|  
|----------------------|----------|------------|------------|-------------|-----------------|-----------------------|--------------|-----------|-------------|---------------|----------|---------|----------|  
|date|1,7|“确定”|-|-|@shouldalert|1,3|1,7|-|确定 (VT_BSTR)|“确定”|“确定”|4|4|  
|Time|5,6,7|-|9|“确定”|6|3,6|5,6|-|确定 (VT_BSTR)|“确定”|“确定”|4|4|  
|Smalldatetime|7|8|9,10|10|“确定”|3|7|-|7 (VT_DATE)|“确定”|“确定”|4|4|  
|DATETIME|5,7|8|9,10|10|“确定”|3|7|-|7 (VT_DATE)|“确定”|“确定”|4|4|  
|Datetime2|5,7|8|9,10|10|7|3|5,7|-|确定 (VT_BSTR)|“确定”|“确定”|4|4|  
|Datetimeoffset|5,7,11|8,11|9,10,11|10,11|7,11|“确定”|5,7,11|-|确定 (VT_BSTR)|“确定”|“确定”|4|4|  
|Char、Varchar、<br /><br /> Nchar、Nvarchar|7, 13|12|12,9|12|12|12|7,13|N/A|N/A|N/A|N/A|N/A|N/A|  
|Sql_variant<br /><br /> (datetime)|7|8|9,10|10|“确定”|3|7|-|7(VT_DATE)|“确定”|“确定”|4|4|  
|Sql_variant<br /><br /> (smalldatetime)|7|8|9,10|10|“确定”|3|7|-|7(VT_DATE)|“确定”|“确定”|4|4|  
|Sql_variant<br /><br /> (date)|1,7|“确定”|2|2|@shouldalert|1,3|1,7|-|OK(VT_BSTR)|“确定”|“确定”|4|4|  
|Sql_variant<br /><br /> (time)|5,6,7|2|6|“确定”|6|3,6|5,6|-|OK(VT_BSTR)|“确定”|“确定”|4|4|  
|Sql_variant<br /><br /> (datetime2)|5,7|8|9,10|10|“确定”|3|5,7|-|OK(VT_BSTR)|“确定”|“确定”|4|4|  
|Sql_variant<br /><br /> (datetimeoffset)|5,7,11|8,11|9,10,11|10,11|7,11|“确定”|5,7,11|-|OK(VT_BSTR)|“确定”|“确定”|4|4|  
  
## <a name="key-to-symbols"></a>符号含义  
  
|符号|含义|  
|------------|-------------|  
|“确定”|不需要任何转换。|  
|-|不支持任何转换。 如果调用 iaccessor:: Createaccessor 时验证绑定，在中返回 DBBINDSTATUS_UPSUPPORTEDCONVERSION *rgStatus*。 当延迟取值函数验证时，则设置 DBSTATUS_E_BADACCESSOR。|  
|@shouldalert|时间字段设置为零。|  
|2|设置 DBSTATUS_E_CANTCONVERTVALUE。|  
|3|时区设置为零。|  
|4|如果客户端缓冲区不够大，则设置 DBSTATUS_S_TRUNCATED。 如果服务器类型包含秒的小数部分，结果字符串中的位数与服务器类型的小数位数完全匹配。|  
|5|截断的秒或秒的小数部分将被忽略。|  
|6|除非源为字符串时间文字，并且目标为 DBTYPE_DATE，否则将日期设置为当前日期。 这种情况下，将使用 1899-12-30。|  
|7|如果值溢出，则设置 DBSTATUS_E_DATAOVERFLOW。|  
|8|忽略时间字段。|  
|9|忽略秒的小数部分字段。|  
|10|忽略日期部分。|  
|11|将时间转换为客户端时区。 如果在此转换过程中出现错误，则设置 DBSTATUS_E_DATAOVERFLOW。|  
|12|字符串分析为 ISO 文字并转换为目标类型。 如果上述操作失败，该字符串则分析为 OLE 日期文字（还包含时间部分），并从 OLE 日期 (DBTYPE_DATE) 转换为目标类型。 字符串必须符合成功分析 ISO 格式所允许的目标类型的文字语法。 若要成功分析 OLE，字符串必须符合可由 OLE 识别的语法。 如果无法分析该字符串，则设置 DBSTATUS_E_CANTCONVERTVALUE。 如果任一部分的值超出范围，则设置 DBSTATUS_E_DATAOVERFLOW。|  
|13|字符串分析为 ISO 文字并转换为目标类型。 如果上述操作失败，该字符串则分析为 OLE 日期文字（还包含时间部分），并从 OLE 日期 (DBTYPE_DATE) 转换为目标类型。 除非目标为 DBTYPE_DATE 或 DBTYPE_DBTIMESTAMP，否则该字符串必须符合日期时间文字的语法。 在这种情况下，允许日期时间或时间文字，以便成功分析 ISO 格式。 若要成功分析 OLE，字符串必须符合可由 OLE 识别的语法。 如果无法分析该字符串，则设置 DBSTATUS_E_CANTCONVERTVALUE。 如果任一部分的值超出范围，则设置 DBSTATUS_E_DATAOVERFLOW。|  
  
## <a name="see-also"></a>请参阅  
 [绑定和转换 (OLE DB)](../../relational-databases/native-client-ole-db-date-time/conversions-ole-db.md)  
  
  
