---
title: 执行从客户端转换到服务器 |Microsoft 文档
description: 执行从客户端到服务器转换
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB], client to server
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fefb80d266e4cd64e65a74c2a70e5a3c36381cd3
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="conversions-performed-from-client-to-server"></a>在客户端和服务器之间执行的转换
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本指南介绍了执行之间的日期/时间转换为 SQL Server 与 OLE DB 驱动程序编写的客户端应用程序和[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]（或更高版本）。  
  
## <a name="conversions"></a>转换  
 本指南介绍了客户端上执行的转换。 如果客户端指定的参数的秒的小数部分精度不同于服务器上定义的精度，那么，客户端转换将在该服务器允许成功执行该操作时导致失败。 具体而言，客户端将对秒的小数部分的任何截断视为错误，而[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]时间到最接近的整数秒数的值舍入。  
  
 如果未调用 ICommandWithParameters::SetParameterInfo，就像它们是将转换 DBTYPE_DBTIMESTAMP 绑定**datetime2**。  
  
|目标 -><br /><br /> From|DBDATE (date)|DBTIME (time)|DBTIME2 (time)|DBTIMESTAMP (smalldatetime)|DBTIMESTAMP (datetime)|DBTIMESTAMP (datetime2)|DBTIMESTAMPOFFSET (datetimeoffset)|STR|WSTR|SQLVARIANT<br /><br /> (sql_variant)|  
|----------------------|---------------------|---------------------|----------------------|-----------------------------------|------------------------------|-------------------------------|------------------------------------------|---------|----------|-------------------------------------|  
|DATE|1, 2|1, 3, 4|4, 12|1, 12|1, 12|1, 12|1, 5, 12|1, 12|1, 12|1, 12<br /><br /> datetime2(0)|  
|DBDATE|1|-|-|1, 6|1, 6|1, 6|1, 5, 6|1, 10|1, 10|1<br /><br /> date|  
|DBTIME|-|1|1|1, 7|1, 7|1, 7|1, 5, 7|1, 10|1, 10|1<br /><br /> Time(0)|  
|DBTIME2|-|1, 3|1|1, 7, 10, 14|1, 7, 10, 15|1, 7, 10|1, 5, 7, 10|1, 10, 11|1, 10, 11|1<br /><br /> Time(7)|  
|DBTIMESTAMP|1, 2|1, 3, 4|1, 4, 10|1, 10, 14|1, 10, 15|1, 10|1, 5, 10|1, 10,11|1, 10, 11|1, 10<br /><br /> datetime2(7)|  
|DBTIMESTAMPOFFSET|1, 2, 8|1, 3, 4, 8|1, 4, 8, 10|1, 8, 10, 14|1, 8, 10, 15|1, 8, 10|1, 10|1, 10, 11|1, 10, 11|1, 10<br /><br /> datetimeoffset(7)|  
|FILETIME|1, 2|1, 3, 4|1, 4, 13|1, 13|1, 13|1, 13|1, 5, 13|1, 13|1, 10|1, 13<br /><br /> datetime2(3)|  
|BYTES|-|-|-|-|-|-|-|N/A|N/A|N/A|  
|VARIANT|1|1|1|1, 10|1, 10|1, 10|1, 10|N/A|N/A|1, 10|  
|SSVARIANT|1, 16|1, 16|1, 16|1, 10, 16|1, 10, 16|1, 10, 16|1, 10, 16|N/A|N/A|1, 16|  
|BSTR|1, 9|1, 9|1, 9, 10|1, 9, 10|1, 9, 10|1, 9, 10|1, 9, 10|N/A|N/A|N/A|  
|STR|1, 9|1, 9|1, 9, 10|1, 9, 10|1, 9, 10|1, 9, 10|1, 9, 10|N/A|N/A|N/A|  
|WSTR|1, 9|1, 9|1, 9, 10|1, 9, 10|1, 9, 10|1, 9, 10|1, 9, 10|N/A|N/A|N/A|  
  
## <a name="key-to-symbols"></a>符号含义  
  
|符号|含义|  
|------------|-------------|  
|-|不支持任何转换。 如果调用 IAccessor::CreateAccessor 时验证绑定，以返回 DBBINDSTATUS_UPSUPPORTEDCONVERSION *rgStatus*。 当延迟取值函数验证时，则设置 DBSTATUS_E_BADACCESSOR。|  
|N/A|不适用。|  
|1|如果提供的数据无效，则设置 DBSTATUS_E_CANTCONVERTVALUE。 在应用转换前验证输入数据，因此即使后续转换忽略某一部分，该部分仍然有效，以使转换成功完成。|  
|2|忽略时间字段。|  
|3|秒的小数部分必须为零，或者设置 DBSTATUS_E_DATAOVERFLOW。|  
|4|忽略日期部分。|  
|5|根据客户端的时区设置设置时区。|  
|6|时间设置为零。|  
|7|日期设置为当前日期。|  
|8|将时间转换为 UTC。 如果在此转换过程中出现错误，则设置 DBSTATUS_E_CANTCONVERTVALUE。|  
|9|字符串分析为 ISO 文字并转换为目标类型。 如果上述操作失败，该字符串则分析为 OLE 日期文字（还包含时间部分），并从 OLE 日期 (DBTYPE_DATE) 转换为目标类型。<br /><br /> 如果目标类型为 DBTIMESTAMP、 **smalldatetime**、 **datetime**或 **datetime2**，字符串必须符合日期、时间或 **datetime2** 文字的语法或 OLE 可识别的语法。 如果字符串为日期文字，所有时间部分将设置为零。 如果字符串为时间文字，则将日期设置为当前日期。<br /><br /> 对于所有其他目标类型，字符串必须符合目标类型的文字语法。|  
|10|如果截断秒的小数部分，且发生数据丢失，则设置 DBSTATUS_E_DATAOVERFLOW。 对于字符串转换，仅当该字符串符合 ISO 语法时才能执行溢出检查。 如果字符串为 OLE 日期文字，则舍入秒的小数部分。<br /><br /> 有关从 DBTIMESTAMP (datetime) 到 smalldatetime OLE DB 驱动程序的 SQL Server 的转换，以及将以无提示方式会截断秒值，而不是引发 DBSTATUS_E_DATAOVERFLOW 错误。|  
|11|下表根据情况下，从目标列的大小确定的小数部分的第二个位数 （缩放）。 对于大于表中范围的列大小，则暗指小数位数为 9。 此转换应允许最高 9 位的秒的小数部分位数，这是 OLE DB 允许的最大位数。<br /><br /> 但是，如果源类型为 DBTIMESTAMP 且秒的小数部分为零，则不会生成秒的小数部分位数或小数点。 此行为确保使用早期 OLE DB 访问接口开发的应用程序的向后兼容性。<br /><br /> 列大小为 ~0 则表示 OLE DB 的大小不受限制（即 9 位数，除非应用 DBTIMESTAMP 的三位数规则）。|  
|12|之前的转换语义[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]DBTYPE_DATE 将在搜索框中保留。 秒的小数部分被截断为零。|  
|13|之前的转换语义[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]DBTYPE_FILETIME 将在搜索框中保留。 如果你使用 Windows FileTimeToSystemTime API，秒的小数部分精度被限制为 1 毫秒。|  
|14|之前的转换语义[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]为**smalldatetime**维护。 秒设置为零。|  
|15|之前的转换语义[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]为**datetime**维护。 秒舍入为最接近的 1/300 秒。|  
|16|嵌入 SSVARIANT 客户端结构的指定类型值的转换行为与未嵌入 SSVARIANT 客户端结构的相同类型和相同值的行为相同。|  
  
||||  
|-|-|-|  
|类型|长度（以字符为单位）|小数位数|  
|DBTIME2|8, 10..18|0,1..9|  
|DBTIMESTAMP|19, 21..29|0,1..9|  
|DBTIMESTAMPOFFSET|26, 28..36|0,1..9|  
  
## <a name="see-also"></a>另请参阅  
 [绑定和转换&#40;OLE DB&#41;](../../oledb/ole-db-date-time/conversions-ole-db.md)  
  
  
