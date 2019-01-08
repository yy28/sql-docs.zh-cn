---
title: 行集和参数中的数据类型映射 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- DBTYPE_SQLVARIANT data type
- SQL Server Native Client OLE DB provider, data types
- rowsets [OLE DB], data type mapping
- data types [OLE DB]
- GetColumnInfo function
- parameters [OLE DB]
- SSPROP_ALLOWNATIVEVARIANT property
- GetParameterInfo function
- OLE DB, data types
ms.assetid: 3d831ff8-3b79-4698-b2c1-2b5dd2f8235c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0979892b6770b9a9c2d0d9c4e8a0d734d873c085
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52766039"
---
# <a name="data-type-mapping-in-rowsets-and-parameters"></a>行集和参数中的数据类型映射
  在行集并作为参数值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序代表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通过使用以下 OLE DB 数据定义数据类型，函数中报告**icolumnsinfo:: Getcolumninfo**和**Icommandwithparameters:: Getparameterinfo**。  
  
|SQL Server 数据类型|OLE DB 数据类型|  
|--------------------------|----------------------|  
|**bigint**|DBTYPE_I8|  
|**binary**|DBTYPE_BYTES|  
|**bit**|DBTYPE_BOOL|  
|**char**|DBTYPE_STR|  
|**datetime**|DBTYPE_DBTIMESTAMP|  
|**datetime2**|DBTYPE_DBTIME2|  
|**decimal**|DBTYPE_NUMERIC|  
|**float**|DBTYPE_R8|  
|**image**|DBTYPE_BYTES|  
|**int**|DBTYPE_I4|  
|**money**|DBTYPE_CY|  
|**nchar**|DBTYPE_WSTR|  
|**ntext**|DBTYPE_WSTR|  
|**numeric**|DBTYPE_NUMERIC|  
|**nvarchar**|DBTYPE_WSTR|  
|**real**|DBTYPE_R4|  
|**smalldatetime**|DBTYPE_DBTIMESTAMP|  
|**smallint**|DBTYPE_I2|  
|**smallmoney**|DBTYPE_CY|  
|**sql_variant**|DBTYPE_VARIANT、DBTYPE_SQLVARIANT|  
|**sysname**|DBTYPE_WSTR|  
|**text**|DBTYPE_STR|  
|**timestamp**|DBTYPE_BYTES|  
|**tinyint**|DBTYPE_UI1|  
|**UDT**|DBTYPE_UDT|  
|**uniqueidentifier**|DBTYPE_GUID|  
|**varbinary**|DBTYPE_BYTES|  
|**varchar**|DBTYPE_STR|  
|**XML**|DBTYPE_XML|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持使用者请求的数据转换，在图中所示。  
  
 sql_variant 对象可以保留除 text、ntext、image、varchar(max)、nvarchar(max)、varbinary(max)、xml、timestamp 和 Microsoft .NET Framework 公共语言运行时 (CLR) 用户定义类型以外的任意 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型的数据。 另外，sql_variant 数据实例还不能将 sql_variant 作为其基础的基本数据类型。 例如，列中的某些行可能包含 smallint 值，而其他某些行可能包含 float 值，剩余的行则包含 char/nchar 值。  
  
> [!NOTE]  
>  **Sql_variant**数据类型是类似于 Variant 数据类型在 Microsoft Visual Basic?? 和 DBTYPE_VARIANT、 DBTYPE_SQLVARIANT OLEDB 中。  
  
 当提取 sql_variant 数据作为 DBTYPE_VARIANT 时，该数据被放置到缓冲区的 VARIANT 结构中。 但 VARIANT 结构中的子类型可能无法映射为 sql_variant 数据类型中定义的子类型。 然后，必须提取 sql_variant 数据作为 DBTYPE_SQLVARIANT，以使所有子类型匹配。  
  
## <a name="dbtypesqlvariant-data-type"></a>DBTYPE_SQLVARIANT 数据类型  
 若要支持**sql_variant**数据类型， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口公开一个名为 DBTYPE_SQLVARIANT 的特定于提供程序的数据类型。 当提取 sql_variant 数据作为 DBTYPE_SQLVARIANT 时，该数据存储到特定于访问接口的 SSVARIANT 结构中。 SSVARIANT 结构包含与 sql_variant 数据类型的子类型匹配的所有子类型。  
  
 此外，还必须将 SSPROP_ALLOWNATIVEVARIANT 会话属性设置为 TRUE。  
  
## <a name="provider-specific-property-sspropallownativevariant"></a>特定于访问接口的 SSPROP_ALLOWNATIVEVARIANT 属性  
 提取数据时，您可以显式指定应为列或参数返回的数据类型。 还可以使用 IColumnsInfo 获取列信息，并将该信息用于绑定。 当使用 IColumnsInfo 获取列信息以用于绑定目的时，如果 SSPROP_ALLOWNATIVEVARIANT 会话属性为 FALSE（默认值），则为 sql_variant 列返回 DBTYPE_VARIANT。 如果 SSPROP_ALLOWNATIVEVARIANT 属性为 FALSE，则不支持 DBTYPE_SQLVARIANT。 如果 SSPROP_ALLOWNATIVEVARIANT 属性设置为 TRUE，列类型将作为 DBTYPE_SQLVARIANT 返回，在这种情况下，缓冲区将保留 SSVARIANT 结构。 在提取 sql_variant 数据作为 DBTYPE_SQLVARIANT 时，必须将 SSPROP_ALLOWNATIVEVARIANT 会话属性设置为 TRUE。  
  
 SSPROP_ALLOWNATIVEVARIANT 属性是特定于访问接口的 DBPROPSET_SQLSERVERSESSION 属性集的一部分，因此，该属性是一个会话属性。  
  
 DBTYPE_VARIANT 适用于所有其他 OLE DB 访问接口。  
  
## <a name="sspropallownativevariant"></a>SSPROP_ALLOWNATIVEVARIANT  
 SSPROP_ALLOWNATIVEVARIANT 是一个会话属性，并且是 DBPROPSET_SQLSERVERSESSION 属性集的一部分。  
  
|||  
|-|-|  
|SSPROP_ALLOWNATIVEVARIANT|键入：VT_BOOL<br /><br /> R/W：读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明:确定在提取的数据是作为 DBTYPE_VARIANT 还是作为 DBTYPE_SQLVARIANT。<br /><br /> VARIANT_TRUE：作为 dbtype_sqlvariant 时，在这种情况下缓冲区将保留 SSVARIANT 结构返回列类型。<br /><br /> VARIANT_FALSE：列类型作为 DBTYPE_VARIANT 返回，并将缓冲区将具有 VARIANT 结构。|  
  
## <a name="see-also"></a>请参阅  
 [数据类型&#40;OLE DB&#41;](data-types-ole-db.md)  
  
  
