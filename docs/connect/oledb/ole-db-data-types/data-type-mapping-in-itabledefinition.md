---
title: 数据类型映射中 ITableDefinition |Microsoft 文档
description: ITableDefinition 中的数据类型映射
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-data-types
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: d613fc7be394bbf16c86c5e217e3dfe83a4296a1
ms.sourcegitcommit: e1bc8c486680e6d6929c0f5885d97d013a537149
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2018
ms.locfileid: "35666347"
---
# <a name="data-type-mapping-in-itabledefinition"></a>ITableDefinition 中的数据类型映射
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  通过使用创建表时**ITableDefinition::CreateTable**函数，可指定的 SQL Server 使用者 OLE DB 驱动程序[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的数据类型*pwszTypeName*的成员传递的 DBCOLUMNDESC 数组。 如果使用者按名称指定列的数据类型，OLE DB 数据类型映射，由表示*wType* DBCOLUMNDESC 结构中，成员将被忽略。  
  
 使用 DBCOLUMNDESC 结构的 OLE DB 数据类型指定新的列数据类型时*wType*成员，SQL Server 的 OLE DB 驱动程序将 OLE DB 数据类型的映射，如下所示。  
  
|OLE DB 数据类型|SQL Server<br /><br /> 数据类型|其他信息|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**二进制**， **varbinary**，**映像，** 或**varbinary （max)**|SQL Server 的 OLE DB 驱动程序检查*ulColumnSize* DBCOLUMNDESC 结构的成员。 基于的值和版本[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例，OLE DB 驱动程序的 SQL Server 映射到类型**映像**。<br /><br /> 如果值*ulColumnSize*小于的最大长度**二进制**数据类型列中，则 SQL Server 的 OLE DB 驱动程序检查 DBCOLUMNDESC *rgPropertySets*成员。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE，SQL Server 的 OLE DB 驱动程序映射到类型**二进制**。 如果属性的值是 VARIANT_FALSE，SQL Server 的 OLE DB 驱动程序映射到类型**varbinary**。 在任一情况下，DBCOLUMNDESC *ulColumnSize*成员确定创建的 SQL Server 列的宽度。|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime2**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**int**||  
|DBTYPE_I4|**int**||  
|DBTYPE_I8|**bigint**||
|DBTYPE_NUMERIC|**numeric**|SQL Server 的 OLE DB 驱动程序检查 DBCOLUMDESC *bPrecision*和*bScale*成员确定精度和扩展，从而**数值**列。|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**， **varchar**，**文本，** 或**varchar （max)**|SQL Server 的 OLE DB 驱动程序检查*ulColumnSize* DBCOLUMNDESC 结构的成员。 基于的值和版本[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例，OLE DB 驱动程序的 SQL Server 映射到类型**文本**。<br /><br /> 如果值*ulColumnSize*小于一个多字节字符数据类型列，然后 OLE DB 驱动程序的最大长度为 SQL Server 检查 DBCOLUMNDESC *rgPropertySets*成员。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE，SQL Server 的 OLE DB 驱动程序映射到类型**char**。 如果属性的值是 VARIANT_FALSE，SQL Server 的 OLE DB 驱动程序映射到类型**varchar**。 在任一情况下，DBCOLUMNDESC *ulColumnSize*成员确定的宽度[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]创建列。|  
|DBTYPE_UDT|**UDT**|在使用以下信息**DBCOLUMNDESC**结构通过**ITableDefinition::CreateTable**需要 UDT 列时：<br /><br /> *pwSzTypeName*将被忽略。<br /><br /> *rgPropertySets*必须包括**DBPROPSET_SQLSERVERCOLUMN**属性设置在上一部分中所述**DBPROPSET_SQLSERVERCOLUMN**中[使用用户定义类型](../../oledb/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_VARIANT|**sql_variant**||
|DBTYPE_WSTR|**nchar**， **nvarchar**， **ntext**或**nvarchar (max)**|SQL Server 的 OLE DB 驱动程序检查*ulColumnSize* DBCOLUMNDESC 结构的成员。 根据值，用于 SQL Server 的 OLE DB 驱动程序映射到类型**ntext**。<br /><br /> 如果值*ulColumnSize*小于 Unicode 字符数据类型列，然后 OLE DB 驱动程序的最大长度为 SQL Server 检查 DBCOLUMNDESC *rgPropertySets*成员。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE，SQL Server 的 OLE DB 驱动程序映射到类型**nchar**。 如果属性的值是 VARIANT_FALSE，SQL Server 的 OLE DB 驱动程序映射到类型**nvarchar**。 在任一情况下，DBCOLUMNDESC *ulColumnSize*成员确定的宽度[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]创建列。|  
|DBTYPE_XML|**XML**||  

> [!NOTE]  
>  在创建新表时，SQL Server 的 OLE DB 驱动程序映射仅 OLE DB 数据类型枚举指定的值上表中。 尝试创建其中某一列为任何其他 OLE DB 数据类型的表时将生成错误。  

## <a name="see-also"></a>请参阅  
 [数据类型&#40;OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
