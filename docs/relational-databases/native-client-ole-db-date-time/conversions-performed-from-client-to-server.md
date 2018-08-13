---
title: 执行从客户端转换到服务器 |Microsoft Docs
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
- conversions [OLE DB], client to server
ms.assetid: 6bb24928-0f3e-4119-beda-cfd04a44a3eb
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: c294fc52ee859ab3ee8c3efb18c7cda59a7e5810
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39562531"
---
# <a name="conversions-performed-from-client-to-server"></a>在客户端和服务器之间执行的转换
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  本主题说明在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 编写的客户端应用程序与 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更高版本）之间执行的日期/时间转换。  
  
## <a name="conversions"></a>转换  
 本主题介绍在客户端上执行的转换。 如果客户端指定的参数的秒的小数部分精度不同于服务器上定义的精度，那么，客户端转换将在该服务器允许成功执行该操作时导致失败。 特别是，客户端将将秒的小数部分的任何截断视为错误，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将时间值舍入为最接近的整数秒数。  
  
 如果未调用 icommandwithparameters:: Setparameterinfo，将转换 DBTYPE_DBTIMESTAMP 绑定，就好像**datetime2**。  
  
|目标 -><br /><br /> From|DBDATE (date)|DBTIME (time)|DBTIME2 (time)|DBTIMESTAMP (smalldatetime)|DBTIMESTAMP (datetime)|DBTIMESTAMP (datetime2)|DBTIMESTAMPOFFSET (datetimeoffset)|STR|WSTR|SQLVARIANT<br /><br /> (sql_variant)|  
|----------------------|---------------------|---------------------|----------------------|-----------------------------------|------------------------------|-------------------------------|------------------------------------------|---------|----------|-------------------------------------|  
|DATE|1,2|1,3,4|4,12|1,12|1,12|1,12|1,5, 12|1,12|1,12|1,12<br /><br /> datetime2(0)|  
|DBDATE|@shouldalert|-|-|1,6|1,6|1,6|1,5, 6|1,10|1,10|@shouldalert<br /><br /> 日期|  
|DBTIME|-|@shouldalert|@shouldalert|1,7|1,7|1,7|1,5, 7|1,10|1,10|@shouldalert<br /><br /> Time(0)|  
|DBTIME2|-|1,3|@shouldalert|1,7,10,14|1,7,10,15|1,7,10|1,5,7,10|1,10,11|1,10,11|@shouldalert<br /><br /> Time(7)|  
|DBTIMESTAMP|1,2|1,3,4|1,4,10|1,10,14|1,10,15|1,10|1,5,10|1,10,11|1,10,11|1,10<br /><br /> datetime2(7)|  
|DBTIMESTAMPOFFSET|1,2,8|1,3,4,8|1,4,8,10|1,8,10,14|1,8,10,15|1,8,10|1,10|1,10,11|1,10,11|1,10<br /><br /> datetimeoffset(7)|  
|FILETIME|1,2|1,3,4|1,4,13|1,13|1,13|1,13|1,5,13|1,13|1,10|1,13<br /><br /> datetime2(3)|  
|BYTES|-|-|-|-|-|-|-|N/A|N/A|N/A|  
|VARIANT|@shouldalert|@shouldalert|@shouldalert|1,10|1,10|1,10|1,10|N/A|N/A|1,10|  
|SSVARIANT|1,16|1,16|1,16|1,10,16|1,10,16|1,10,16|1,10,16|N/A|N/A|1,16|  
|BSTR|1,9|1,9|1,9,10|1,9,10|1,9,10|1,9,10|1,9,10|N/A|N/A|N/A|  
|STR|1,9|1,9|1,9,10|1,9,10|1,9,10|1,9,10|1,9,10|N/A|N/A|N/A|  
|WSTR|1,9|1,9|1,9,10|1,9,10|1,9,10|1,9,10|1,9,10|N/A|N/A|N/A|  
  
## <a name="key-to-symbols"></a>符号含义  
  
|符号|含义|  
|------------|-------------|  
|-|不支持任何转换。 如果调用 iaccessor:: Createaccessor 时验证绑定，在中返回 DBBINDSTATUS_UPSUPPORTEDCONVERSION *rgStatus*。 当延迟取值函数验证时，则设置 DBSTATUS_E_BADACCESSOR。|  
|N/A|不适用。|  
|@shouldalert|如果提供的数据无效，则设置 DBSTATUS_E_CANTCONVERTVALUE。 在应用转换前验证输入数据，因此即使后续转换忽略某一部分，该部分仍然有效，以使转换成功完成。|  
|2|忽略时间字段。|  
|3|秒的小数部分必须为零，或者设置 DBSTATUS_E_DATAOVERFLOW。|  
|4|忽略日期部分。|  
|5|根据客户端的时区设置设置时区。|  
|6|时间设置为零。|  
|7|日期设置为当前日期。|  
|8|将时间转换为 UTC。 如果在此转换过程中出现错误，则设置 DBSTATUS_E_CANTCONVERTVALUE。|  
|9|字符串分析为 ISO 文字并转换为目标类型。 如果上述操作失败，该字符串则分析为 OLE 日期文字（还包含时间部分），并从 OLE 日期 (DBTYPE_DATE) 转换为目标类型。<br /><br /> 如果目标类型为 DBTIMESTAMP、 **smalldatetime**、 **datetime**或 **datetime2**，字符串必须符合日期、时间或 **datetime2** 文字的语法或 OLE 可识别的语法。 如果字符串为日期文字，所有时间部分将设置为零。 如果字符串为时间文字，则将日期设置为当前日期。<br /><br /> 对于所有其他目标类型，字符串必须符合目标类型的文字语法。|  
|10|如果截断秒的小数部分，且发生数据丢失，则设置 DBSTATUS_E_DATAOVERFLOW。 对于字符串转换，仅当该字符串符合 ISO 语法时才能执行溢出检查。 如果字符串为 OLE 日期文字，则舍入秒的小数部分。<br /><br /> 对于从 DBTIMESTAMP (datetime) 到 smalldatetime 的转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 将自行截断秒值而不引发 DBSTATUS_E_DATAOVERFLOW 错误。|  
|11|秒的小数部分的位数（小数位数）根据下表的目标列的大小确定。 对于大于表中范围的列大小，则暗指小数位数为 9。 此转换应允许最高 9 位的秒的小数部分位数，这是 OLE DB 允许的最大位数。<br /><br /> 但是，如果源类型为 DBTIMESTAMP 且秒的小数部分为零，则不会生成秒的小数部分位数或小数点。 此行为确保使用早期 OLE DB 访问接口开发的应用程序的向后兼容性。<br /><br /> 列大小为 ~0 则表示 OLE DB 的大小不受限制（即 9 位数，除非应用 DBTIMESTAMP 的三位数规则）。|  
|12|将保留 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 之前的 DBTYPE_DATE 转换语义。 秒的小数部分被截断为零。|  
|13|将保留 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 之前的 DBTYPE_FILETIME 转换语义。 如果使用 Windows FileTimeToSystemTime API，秒的小数部分精度则限制为 1 毫秒。|  
|14|将保留 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 之前的 smalldatetime 转换语义。 秒设置为零。|  
|15|将保留 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 之前的 datetime 转换语义。 秒舍入为最接近的 1/300 秒。|  
|16|嵌入 SSVARIANT 客户端结构的指定类型值的转换行为与未嵌入 SSVARIANT 客户端结构的相同类型和相同值的行为相同。|  
  
||||  
|-|-|-|  
|类型|长度（以字符为单位）|小数位数|  
|DBTIME2|8, 10..18|0,1..9|  
|DBTIMESTAMP|19, 21..29|0,1..9|  
|DBTIMESTAMPOFFSET|26, 28..36|0,1..9|  
  
## <a name="see-also"></a>请参阅  
 [绑定和转换 (OLE DB)](../../relational-databases/native-client-ole-db-date-time/conversions-ole-db.md)  
  
  
