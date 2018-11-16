---
title: SSVARIANT 结构 |Microsoft Docs
description: OLE DB 驱动程序中的 SQL Server 的 SSVARIANT 结构
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: d500dc56ff128029ebba1576a84919f9694d8903
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51602227"
---
# <a name="ssvariant-structure"></a>SSVARIANT 结构
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **SSVARIANT**结构，其定义中 msoledbsql.h，对应于 OLE DB 驱动程序中的 DBTYPE_SQLVARIANT 值适用于 SQL Server。  
  
 **SSVARIANT**是区分的联合。 根据 vt 成员的值，使用者可以确定要读取的成员。 vt 值与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型相对应。 因此，SSVARIANT 结构可以具有任何 SQL Server 类型。 有关标准 OLE DB 类型的数据结构的详细信息，请参阅[类型指示符](https://go.microsoft.com/fwlink/?LinkId=122171)。  
  
## <a name="remarks"></a>Remarks  
 如果 DataTypeCompat==80，几个 SSVARIANT 子类型都将成为字符串。 例如，以下 vt 值将在 SSVARIANT 中显示为 VT_SS_WVARSTRING：  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 如果 DateTypeCompat == 0，这些类型将按它们原来的形式显示。  
  
 有关 SSPROP_INIT_DATATYPECOMPATIBILITY 的详细信息，请参阅[OLE DB 驱动程序适用于 SQL Server 连接字符串关键字](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。  
  
 msoledbsql.h 文件包含变量访问宏，可以简化 SSVARIANT 结构中成员类型的取消引用操作。 例如 V_SS_DATETIMEOFFSET，您可以按如下方式使用它：  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 每个成员的完整集的访问宏**SSVARIANT**结构，请参考 msoledbsql.h 文件。  
  
 下表介绍了 SSVARIANT 结构的成员：  
  
|成员|OLE DB 类型指示器|OLE DB C 数据类型|vt 值|注释|  
|------------|---------------------------|------------------------|--------------|--------------|  
|vt|SSVARTYPE|||指定 SSVARIANT 结构中包含的值类型。|  
|bTinyIntVal|DBTYPE_UI1|**BYTE**|**VT_SS_UI1**|支持**tinyint** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型。|  
|sShortIntVal|DBTYPE_I2|**SHORT**|**VT_SS_I2**|支持**smallint** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型。|  
|lIntVal|DBTYPE_I4|**LONG**|**VT_SS_I4**|支持**int** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型。|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|支持**bigint** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型。|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|支持**真实**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型。|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|支持**float** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型。|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|支持**资金**并**smallmoney** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型。|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|支持**位**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型。|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|支持**uniqueidentifier** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型。|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|支持**数值**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型。|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|支持 date[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型。|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|支持**smalldatetime**， **datetime**，并**datetime2** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型。|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|支持**时间**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型。<br /><br /> 包括以下成员：<br /><br /> *tTime2Val* (**DBTIME2**)<br /><br /> *bScale* (**字节**) 指定的小数位数*tTime2Val*值。|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|支持**datetime2** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型。<br /><br /> 包括以下成员：<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (**字节**) 指定的小数位数*tsDataTimeVal*值。|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|支持**datetimeoffset** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型。<br /><br /> 包括以下成员：<br /><br /> *tsoDateTimeOffsetVal* (**DBTIMESTAMPOFFSET**)<br /><br /> *bScale* (**字节**) 指定的小数位数*tsoDateTimeOffsetVal*值。|  
|NCharVal|没有对应的 OLE DB 类型指示器。|**结构 _NCharVal**|**VT_SS_WVARSTRING，**<br /><br /> **VT_SS_WSTRING**|支持**nchar**并**nvarchar** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型。<br /><br /> 包括以下成员：<br /><br /> *sActualLength* (**短**) 指定的字符串的实际长度*pwchNCharVal*点。 不包括尾零。<br /><br /> *sMaxLength* (**短**) 指定的字符串的最大长度*pwchNCharVal*点。<br /><br /> *pwchNCharVal* (**WCHAR** \*) 指向的字符串。<br /><br /> 未使用的成员： *rgbReserved*， *dwReserved*，并*pwchReserved*。|  
|CharVal|没有对应的 OLE DB 类型指示器。|**结构 _CharVal**|**VT_SS_STRING，**<br /><br /> **VT_SS_VARSTRING**|支持**char**并**varchar** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型。<br /><br /> 包括以下成员：<br /><br /> *sActualLength* (**短**) 指定的字符串的实际长度*pchCharVal*点。 不包括尾零。<br /><br /> *sMaxLength* (**短**) 指定的字符串的最大长度*pchCharVal*点。<br /><br /> *pchCharVal* (**CHAR** \*) 指向的字符串。<br /><br /> 不使用的成员：<br /><br /> *rgbReserved*， *dwReserved*，和*pwchReserved*。|  
|BinaryVal|没有对应的 OLE DB 类型指示器。|**结构 _BinaryVal**|**VT_SS_VARBINARY，**<br /><br /> **VT_SS_BINARY**|支持**二进制**并**varbinary** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型。<br /><br /> 包括以下成员：<br /><br /> *sActualLength* (**短**) 指定的数据的实际长度*prgbBinaryVal*点。<br /><br /> *sMaxLength* (**短**) 指定的数据的最大长度*prgbBinaryVal*点。<br /><br /> *prgbBinaryVal* (**字节** \*) 的二进制数据的指针。<br /><br /> 未使用的成员： *dwReserved*。|  
|UnknownType|不使用|不使用|不使用|不使用|  
|BLOBType|不使用|不使用|不使用|不使用|  
  
## <a name="see-also"></a>另请参阅  
 [数据类型&#40;OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
