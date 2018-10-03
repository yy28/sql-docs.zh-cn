---
title: ITableDefinition 中的数据类型映射 |Microsoft Docs
description: ITableDefinition 中的数据类型映射
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- OLE DB Driver for SQL Server, data types
- ITableDefinition interface
- DBCOLUMNDESC structure
- data types [OLE DB]
- CreateTable function
- OLE DB, data types
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 4101c458b066ec34f010a5733510fb21e25e6840
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47834185"
---
# <a name="data-type-mapping-in-itabledefinition"></a>ITableDefinition 中的数据类型映射
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  当使用 ITableDefinition::CreateTable 函数创建表时，适用于 SQL Server 的 OLE DB 驱动程序使用者可以在向其传递的 DBCOLUMNDESC 数组的 pwszTypeName 成员中指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型。 如果使用者按照名称指定列的数据类型，则忽略由 DBCOLUMNDESC 结构的 wType 成员表示的 OLE DB 数据类型映射。  
  
 当使用 DBCOLUMNDESC 结构的 wType 成员指定具有 OLE DB 数据类型的新列数据类型时，适用于 SQL Server 的 OLE DB 驱动程序将按以下方式映射 OLE DB 数据类型。  
  
|OLE DB 数据类型|SQL Server<br /><br /> 数据类型|其他信息|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|binary、varbinary、image 或 varbinary(max)|SQL Server 的 OLE DB 驱动程序会检查*ulColumnSize* DBCOLUMNDESC 结构的成员。 基于值和版本[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例，OLE DB 驱动程序的 SQL Server 将映射到类型**映像**。<br /><br /> 如果 ulColumnSize 的值小于 binary 数据类型列的最大长度，则适用于 SQL Server 的 OLE DB 驱动程序将检查 DBCOLUMNDESC 的 rgPropertySets 成员。 如果 DBPROP_COL_FIXEDLENGTH 为 VARIANT_TRUE 时，SQL Server 的 OLE DB 驱动程序将为该类型映射**二进制**。 如果属性的值为 VARIANT_FALSE，SQL Server 的 OLE DB 驱动程序将为该类型映射**varbinary**。 在这两种情况下，DBCOLUMNDESC 的 ulColumnSize 成员将确定创建的 SQL Server 列的宽度。|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime2**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_I8|**bigint**||
|DBTYPE_NUMERIC|**numeric**|适用于 SQL Server 的 OLE DB 驱动程序检查 DBCOLUMDESC 的 bPrecision 和 bScale 成员以确定 numeric 列的精度和小数位数。|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|char、varchar、text 或 varchar(max)|SQL Server 的 OLE DB 驱动程序会检查*ulColumnSize* DBCOLUMNDESC 结构的成员。 基于值和版本[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例，OLE DB 驱动程序的 SQL Server 将映射到类型**文本**。<br /><br /> 如果 ulColumnSize 的值小于 multibyte 数据类型列的最大长度，则适用于 SQL Server 的 OLE DB 驱动程序将检查 DBCOLUMNDESC 的 rgPropertySets 成员。 如果 DBPROP_COL_FIXEDLENGTH 为 VARIANT_TRUE 时，SQL Server 的 OLE DB 驱动程序将为该类型映射**char**。 如果属性的值为 VARIANT_FALSE，SQL Server 的 OLE DB 驱动程序将为该类型映射**varchar**。 在这两种情况下，DBCOLUMNDESC ulColumnSize 成员将确定创建的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 列的宽度。|  
|DBTYPE_UDT|**UDT**|需要 UDT 列时，ITableDefinition::CreateTable 将在 DBCOLUMNDESC 结构中用到以下信息：<br /><br /> *pwSzTypeName*将被忽略。<br /><br /> *rgPropertySets*必须包含**DBPROPSET_SQLSERVERCOLUMN**属性设置在上一部分中所述**DBPROPSET_SQLSERVERCOLUMN**中[使用用户定义类型](../../oledb/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_VARIANT|**sql_variant**||
|DBTYPE_WSTR|nchar、nvarchar、ntext 或 nvarchar(max)|SQL Server 的 OLE DB 驱动程序会检查*ulColumnSize* DBCOLUMNDESC 结构的成员。 基于值，用于 SQL Server 的 OLE DB 驱动程序将该类型映射到**ntext**。<br /><br /> 如果 ulColumnSize 的值小于 Unicode 数据类型列的最大长度，则适用于 SQL Server 的 OLE DB 驱动程序将检查 DBCOLUMNDESC 的 rgPropertySets 成员。 如果 DBPROP_COL_FIXEDLENGTH 为 VARIANT_TRUE 时，SQL Server 的 OLE DB 驱动程序将为该类型映射**nchar**。 如果属性的值为 VARIANT_FALSE，SQL Server 的 OLE DB 驱动程序将为该类型映射**nvarchar**。 在这两种情况下，DBCOLUMNDESC ulColumnSize 成员将确定创建的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 列的宽度。|  
|DBTYPE_XML|**XML**||  

> [!NOTE]  
>  创建新表时，适用于 SQL Server 的 OLE DB 驱动程序只映射前一个表中指定的 OLE DB 数据类型枚举值。 尝试创建其中某一列为任何其他 OLE DB 数据类型的表时将生成错误。  

## <a name="see-also"></a>另请参阅  
 [数据类型&#40;OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
