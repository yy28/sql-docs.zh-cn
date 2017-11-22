---
title: "增强的日期和时间类型 （OLE DB 和 ODBC） 进行大容量复制更改 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-date-time
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: ODBC, bulk copy operations
ms.assetid: c29e0f5e-9b3c-42b3-9856-755f4510832f
caps.latest.revision: "27"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: da9c9153c30e45eaa821c367f5a8b627078f7a9c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc"></a>增强的日期和时间类型 （OLE DB 和 ODBC） 的大容量复制更改
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  本主题描述为支持大容量复制功能而增强的日期/时间功能。 本主题中的信息对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 中的 OLE DB 和 ODBC 均适用。  
  
## <a name="format-files"></a>格式化文件  
 在以交互方式生成格式化文件时，下表描述用于指定日期/时间类型和相应的宿主文件数据类型名称的输入。  
  
|文件存储类型|宿主文件数据类型|对提示符的响应:"输入文件存储类型的字段 < 字段名 > [\<默认 >]:"|  
|-----------------------|-------------------------|-----------------------------------------------------------------------------------------------------|  
|日期时间|SQLDATETIME|d|  
|Smalldatetime|SQLDATETIM4|D|  
|日期|SQLDATE|de|  
|Time|SQLTIME|te|  
|Datetime2|SQLDATETIME2|d2|  
|Datetimeoffset|SQLDATETIMEOFFSET|do|  
  
 XML 格式化文件 XSD 将增加以下内容：  
  
```  
<xs:complexType name="SQLDATETIME2">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATETIMEOFFSET">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATE">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLTIME">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
```  
  
## <a name="character-data-files"></a>字符数据文件  
 在字符数据文件中，日期和时间值表示的"数据格式:: 字符串和文本"部分中所述[ODBC 日期和时间的改进的数据类型支持](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)适用于 ODBC 或[数据类型支持OLE DB 日期和时间改进](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)用于 OLE DB。  
  
 在本机数据文件为四种新类型的日期和时间值表示为对应 TDS 的表示形式是小数位数为 7 (因为这是支持的最大[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 bcp 数据文件不存储这些列的小数位数)。 不没有到现有的存储的任何更改**datetime**和**smalldatetime**类型或其表格数据流式处理 (TDS) 表示形式。  
  
 针对 OLE DB 的不同存储类型的存储大小如下：  
  
|文件存储类型|存储大小（以字节为单位）|  
|-----------------------|---------------------------|  
|datetime|8|  
|smalldatetime|4|  
|date|3|  
|time|6|  
|datetime2|9|  
|datetimeoffset|11|  
  
 针对 ODBC 的大小如下。 请注意，不必在格式化文件或数据文件中存储精度，因为 BCP.exe 将始终从服务器检索精度。  
  
|文件存储类型|存储大小（以字节为单位）|存储格式|  
|-----------------------|---------------------------|--------------------|  
|datetime (d)|8|TDS|  
|smalldatetime (D)|4|TDS|  
|date (de)|3|TDS|  
|time (te)|6|TDS|  
|datetime2 (d2)|9|TDS|  
|datetimeoffset (do)|11|TDS|  
  
## <a name="bcp-types-in-sqlnclih"></a>sqlncli.h 中的 BCP 类型  
 以下类型在 sqlncli.h 中定义，以便用于对 ODBC 的 BCP API 扩展。 这些类型会随同传递*eUserDataType* IBCPSession::BCPColFmt OLE DB 中的参数。  
  
|文件存储类型|宿主文件数据类型|键入用于 IBCPSession::BCPColFmt 中|值|  
|-----------------------|-------------------------|-----------------------------------------------------------|-----------|  
|日期时间|SQLDATETIME|BCP_TYPE_SQLDATETIME|0x3d|  
|Smalldatetime|SQLDATETIM4|BCP_TYPE_SQLDATETIME4|0x3a|  
|日期|SQLDATE|BCP_TYPE_SQLDATE|0x28|  
|Time|SQLTIME|BCP_TYPE_SQLTIME|0x29|  
|Datetime2|SQLDATETIME2|BCP_TYPE_SQLDATETIME2|0x2a|  
|Datetimeoffset|SQLDATETIMEOFFSET|BCP_TYPE_SQLDATETIMEOFFSET|0x2b|  
  
## <a name="bcp-data-type-conversions"></a>BCP 数据类型转换  
 下表提供转换信息。  
  
 **OLE DB 注意**的 IBCPSession 来执行以下转换。 IRowsetFastLoad 使用 OLE DB 转换中定义[转换执行从客户端到服务器](../../relational-databases/native-client-ole-db-date-time/conversions-performed-from-client-to-server.md)。 请注意，日期时间值将舍入为 1 秒的 1/300，smalldatetime 值在执行下述客户端转换后将秒设置为零。 日期时间舍入将传播至小时和分钟，而非日期。  
  
|若要：<br /><br /> From|date|time|smalldatetime|datetime|datetime2|datetimeoffset|char|wchar|  
|------------------------|----------|----------|-------------------|--------------|---------------|--------------------|----------|-----------|  
|日期|1|-|1,6|1,6|1,6|1,5,6|1,3|1,3|  
|Time|N/A|1,10|1,7,10|1,7,10|1,7,10|1,5,7,10|1,3|1,3|  
|Smalldatetime|1,2|1,4,10|1|1|1,10|1,5,10|1,11|1,11|  
|日期时间|1,2|1,4,10|1,12|1|1,10|1,5,10|1,11|1,11|  
|Datetime2|1,2|1,4,10|1,10 (ODBC)1,12 (OLE DB)|1,10|1,10|1,5,10|1,3|1,3|  
|Datetimeoffset|1,2,8|1,4,8,10|1,8,10|1,8,10|1,8,10|1,10|1,3|1,3|  
|Char/wchar (date)|9|-|9,6 (ODBC)9,6,12 (OLE DB)|9,6 (ODBC)9,6,12 (OLE DB)|9,6|9,5,6|N/A|N/A|  
|Char/wchar (time)|-|9,10|9,7,10 (ODBC)9,7,10,12 (OLE DB)|9,7,10 (ODBC)9,7,10, 12 (OLE DB)|9,7,10|9,5,7,10|N/A|N/A|  
|Char/wchar (datetime)|9,2|9,4,10|9,10 (ODBC)9,10,12 (OLE DB)|9,10 (ODBC)9,10,12 (OLE DB)|9,10|9,5,10|N/A|N/A|  
|Char/wchar (datetimeoffset)|9,2,8|9,4,8,10|9,8,10 (ODBC)9,8,10,12 (OLE DB)|9,8,10 (ODBC)9,8,10,12 (OLE DB)|9,8,10|9,10|N/A|N/A|  
  
#### <a name="key-to-symbols"></a>符号含义  
  
|符号|含义|  
|------------|-------------|  
|-|不支持任何转换。<br /><br /> 生成 ODBC 诊断记录，同时还生成 SQLSTATE 07006 和消息“受限制的数据类型属性冲突”。|  
|1|如果提供的数据无效，则生成 ODBC 诊断记录，同时还生成 SQLSTATE 22007 和消息“日期时间格式无效”。 对于 datetimeoffset 值，在转换为 UTC 后时间部分必须处于规定范围内，即使不要求转换为 UTC。 这是因为 TDS 和服务器始终规范化 UTC 的 datetimeoffset 值中的时间。 因此，在转换为 UTC 后，客户端必须检查时间部分是否处于支持的范围内。|  
|2|忽略时间部分。|  
|3|对于 ODBC，如果发生具有数据丢失的截断，将生成一个诊断记录，同时还生成 SQLSTATE 22001 和消息“字符串数据，右端被截断”。秒的小数形式位数（小数位数）根据下表的目标列的大小确定。 对于大于表中范围的列大小，则暗指小数位数为 7。 此转换应允许最高 9 位的秒的小数形式位数，这是 ODBC 允许的最大位数。<br /><br /> **类型：** DBTIME2<br /><br /> **隐式小数位数 0** 8<br /><br /> **隐式缩放 1..7** 10,16<br /><br /> <br /><br /> **类型：** DBTIMESTAMP<br /><br /> **隐式小数位数 0:** 19<br /><br /> **隐式缩放 1..7:** 21..27<br /><br /> <br /><br /> **类型：** DBTIMESTAMPOFFSET<br /><br /> **隐式小数位数 0:** 26<br /><br /> **隐式缩放 1..7:** 28..34<br /><br /> 对于 OLE DB，如果发生具有数据丢失的截断，则会发出错误。 对于 datetime2，秒的小数形式位数（小数位数）根据下表的目标列的大小确定。 对于大于表中范围的列大小，则暗指小数位数为 9。 此转换应允许最高 9 位的秒的小数部分位数，这是 OLE DB 允许的最大位数。<br /><br /> **类型：** DBTIME2<br /><br /> **隐式小数位数 0** 8<br /><br /> **隐式缩放 1..9** 1..9<br /><br /> <br /><br /> **类型：** DBTIMESTAMP<br /><br /> **隐式小数位数 0:** 19<br /><br /> **隐式缩放 1..9:** 21..29<br /><br /> <br /><br /> **类型：** DBTIMESTAMPOFFSET<br /><br /> **隐式小数位数 0:** 26<br /><br /> **隐式缩放 1..9:** 28..36|  
|4|忽略日期部分。|  
|5|时区设置为 UTC（例如 00:00）。|  
|6|时间设置为零。|  
|7|日期设置为 1900-01-01。|  
|8|忽略时区偏移量。|  
|9|根据遇到的第一个标点符号以及出现的剩余部分，该字符串将被分析和转换为 date、datetime、datetimeoffset 或 time 值。 然后，根据本主题末尾的表中针对此过程发现的源类型的规则，此字符串将转换为目标类型。 如果提供的数据不能在分析时无错，或者任何组成部分超出允许的范围，或者不存在从文字类型到目标类型的转换，则发出错误 (OLE DB)，或者生成 ODBC 诊断记录，同时还生成 SQLSTATE 22018 和消息“为转换指定的字符值无效”。 对于 datetime 和 smalldatetime 参数，如果年份处于这些类型支持的范围外，则发出错误 (OLE DB)，或者生成 ODBC 诊断记录，同时还生成 SQLSATE 22007 和消息“日期时间格式无效”。<br /><br /> 对于 datetimeoffset，在转换为 UTC 后该值必须处于规定范围内，即使不要求转换为 UTC。 这是因为 TDS 和服务器始终规范化 UTC 的 datetimeoffset 值中的时间，因此在转换为 UTC 后，客户端必须确认时间部分处于支持的范围内。 如果该值不在支持的 UTC 范围内，则发出错误 (OLE DB)，或者生成 ODBC 诊断记录，同时还生成 SQLSTATE 22007 和消息“日期时间格式无效”。|  
|10|如果在客户端到服务器转换时发生具有数据丢失的截断，则发出错误 (OLE DB)，或者生成 ODBC 诊断记录，同时还生成 SQLSTATE 22008 和消息“日期时间字段溢出”。 如果值处于服务器使用的 UTC 范围可表示的范围外，也会发生此错误。 如果在服务器到客户端转换时发生秒或秒的小数部分截断，则只会显示警告。|  
|11|如果发生具有数据丢失的截断，则生成诊断记录。<br /><br /> 在服务器到客户端转换时，这是警告 (ODBC SQLSTATE S1000)。<br /><br /> 在客户端到服务器转换时，这是错误 (ODBC SQLSTATE 22001)。|  
|12|秒设置为零，秒的小数部分被放弃。 可能没有截断错误。|  
|N/A|现有 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更早版本的行为将保持。|  
  
## <a name="see-also"></a>另请参阅  
 [日期和时间改进 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)   
 [日期和时间改进 &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
