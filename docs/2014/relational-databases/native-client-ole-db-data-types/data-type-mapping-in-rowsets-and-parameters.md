---
title: 行集和参数中的数据类型映射 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
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
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77b7718febb0a6b8e8a8575ff776ffb44364b68a
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37422676"
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
|**int**|DBTYPE_I2|  
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
  
 **Sql_variant**对象可以保存的任何数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]除 text、 ntext、 image、 varchar （max）、 nvarchar （max）、 varbinary （max）、 xml、 时间戳和 Microsoft.NET Framework 公共语言运行时 (CLR) 数据类型用户定义类型。 另外，sql_variant 数据实例还不能将 sql_variant 作为其基础的基本数据类型。 例如，列可以包含**smallint**某些行的值**float**其他行的值并**char**/**nchar**其余部分中的值。  
  
> [!NOTE]  
>  **Sql_variant**数据类型是类似于 Microsoft Visual Basic® 和 DBTYPE_VARIANT、 DBTYPE_SQLVARIANT OLEDB 中的 Variant 数据类型。  
  
 当**sql_variant**作为 DBTYPE_VARIANT 提取数据、 放入缓冲区中的 VARIANT 结构。 但 VARIANT 结构中的子类型可能无法映射为子类型中定义**sql_variant**数据类型。 **Sql_variant**必须然后提取数据作为 dbtype_sqlvariant 时按顺序以匹配的所有子类型。  
  
## <a name="dbtypesqlvariant-data-type"></a>DBTYPE_SQLVARIANT 数据类型  
 若要支持**sql_variant**数据类型， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口公开一个名为 DBTYPE_SQLVARIANT 的特定于提供程序的数据类型。 当**sql_variant**作为 dbtype_sqlvariant 时提取数据，它将存储在特定于访问接口的 SSVARIANT 结构。 SSVARIANT 结构包含所有匹配的子类型的子**sql_variant**数据类型。  
  
 此外，还必须将 SSPROP_ALLOWNATIVEVARIANT 会话属性设置为 TRUE。  
  
## <a name="provider-specific-property-sspropallownativevariant"></a>特定于访问接口的 SSPROP_ALLOWNATIVEVARIANT 属性  
 提取数据时，您可以显式指定应为列或参数返回的数据类型。 **IColumnsInfo**还可用来获取列信息并使用它来执行绑定。 当**IColumnsInfo**用来获取列信息进行绑定时，如果 SSPROP_ALLOWNATIVEVARIANT 会话属性为 FALSE （默认值），为返回 DBTYPE_VARIANT **sql_variant**列。 如果 SSPROP_ALLOWNATIVEVARIANT 属性为 FALSE，则不支持 DBTYPE_SQLVARIANT。 如果 SSPROP_ALLOWNATIVEVARIANT 属性设置为 TRUE，列类型将作为 DBTYPE_SQLVARIANT 返回，在这种情况下，缓冲区将保留 SSVARIANT 结构。 在提取**sql_variant**数据作为 dbtype_sqlvariant 时，SSPROP_ALLOWNATIVEVARIANT 会话属性必须设置为 TRUE。  
  
 SSPROP_ALLOWNATIVEVARIANT 属性是特定于访问接口的 DBPROPSET_SQLSERVERSESSION 属性集的一部分，因此，该属性是一个会话属性。  
  
 DBTYPE_VARIANT 适用于所有其他 OLE DB 访问接口。  
  
## <a name="sspropallownativevariant"></a>SSPROP_ALLOWNATIVEVARIANT  
 SSPROP_ALLOWNATIVEVARIANT 是一个会话属性，并且是 DBPROPSET_SQLSERVERSESSION 属性集的一部分。  
  
|||  
|-|-|  
|SSPROP_ALLOWNATIVEVARIANT|类型：VT_BOOL<br /><br /> R/W：读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：确定提取的数据是作为 DBTYPE_VARIANT 还是作为 DBTYPE_SQLVARIANT。<br /><br /> VARIANT_TRUE：列类型作为 DBTYPE_SQLVARIANT 返回，这种情况下缓冲区将保留 SSVARIANT 结构。<br /><br /> VARIANT_FALSE：列类型作为 DBTYPE_VARIANT 返回，且缓冲区将具有 VARIANT 结构。|  
  
## <a name="see-also"></a>请参阅  
 [数据类型&#40;OLE DB&#41;](data-types-ole-db.md)  
  
  
