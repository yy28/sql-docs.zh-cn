---
title: 行集和参数中的数据类型映射 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 48fd34103d517a27e179ede68751b2c0718ea8ba
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024324"
---
# <a name="data-type-mapping-in-rowsets-and-parameters"></a>行集和参数中的数据类型映射
  在行集并为参数值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序表示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通过使用以下 OLE DB 的数据定义的数据类型，在函数中报告**IColumnsInfo::GetColumnInfo**和**ICommandWithParameters::GetParameterInfo**。  
  
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
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持使用者请求数据转换，如图所示。  
  
 **Sql_variant**对象可以保存数据的任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型除外文本、 ntext、 图像、 varchar （max）、 nvarchar (max)、 varbinary （max）、 xml、 时间戳和 Microsoft.NET Framework 公共语言运行时 (CLR)用户定义的类型。 另外，sql_variant 数据实例还不能将 sql_variant 作为其基础的基本数据类型。 例如，列可以包含**smallint**某些行的值**float**其他行的值和**char**/**nchar**的其余部分中的值。  
  
> [!NOTE]  
>  **Sql_variant**数据类型是类似于在 Microsoft Visual Basic® 和 DBTYPE_VARIANT、 DBTYPE_SQLVARIANT 中 OLEDB Variant 数据类型。  
  
 当**sql_variant**作为 DBTYPE_VARIANT 提取数据，它将放入缓冲区中的变体结构。 变体结构中的子类型可能不会映射到在中定义的子类型，但**sql_variant**数据类型。 **Sql_variant**数据必须然后提取作为 DBTYPE_SQLVARIANT 顺序以匹配的所有子类型。  
  
## <a name="dbtypesqlvariant-data-type"></a>DBTYPE_SQLVARIANT 数据类型  
 若要支持**sql_variant**数据类型， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序公开了调用 DBTYPE_SQLVARIANT 一个提供程序特定数据类型。 当**sql_variant**作为 DBTYPE_SQLVARIANT 提取数据，它存储在提供程序特定 SSVARIANT 结构。 SSVARIANT 结构包含所有匹配的子类型的子类型**sql_variant**数据类型。  
  
 此外，还必须将 SSPROP_ALLOWNATIVEVARIANT 会话属性设置为 TRUE。  
  
## <a name="provider-specific-property-sspropallownativevariant"></a>特定于访问接口的 SSPROP_ALLOWNATIVEVARIANT 属性  
 提取数据时，您可以显式指定应为列或参数返回的数据类型。 **IColumnsInfo**还可获取列信息并使用它进行绑定。 当**IColumnsInfo**用来获取列信息出于绑定目的，如果属性为 FALSE （默认值），SSPROP_ALLOWNATIVEVARIANT 会话，将返回 DBTYPE_VARIANT **sql_variant**列。 如果 SSPROP_ALLOWNATIVEVARIANT 属性为 FALSE，则不支持 DBTYPE_SQLVARIANT。 如果 SSPROP_ALLOWNATIVEVARIANT 属性设置为 TRUE，列类型将作为 DBTYPE_SQLVARIANT 返回，在这种情况下，缓冲区将保留 SSVARIANT 结构。 在提取**sql_variant**数据作为 DBTYPE_SQLVARIANT，会话属性 SSPROP_ALLOWNATIVEVARIANT 必须设置为 TRUE。  
  
 SSPROP_ALLOWNATIVEVARIANT 属性是特定于访问接口的 DBPROPSET_SQLSERVERSESSION 属性集的一部分，因此，该属性是一个会话属性。  
  
 DBTYPE_VARIANT 适用于所有其他 OLE DB 访问接口。  
  
## <a name="sspropallownativevariant"></a>SSPROP_ALLOWNATIVEVARIANT  
 SSPROP_ALLOWNATIVEVARIANT 是一个会话属性，并且是 DBPROPSET_SQLSERVERSESSION 属性集的一部分。  
  
|||  
|-|-|  
|SSPROP_ALLOWNATIVEVARIANT|类型：VT_BOOL<br /><br /> R/W：读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：确定提取的数据是作为 DBTYPE_VARIANT 还是作为 DBTYPE_SQLVARIANT。<br /><br /> VARIANT_TRUE：列类型作为 DBTYPE_SQLVARIANT 返回，这种情况下缓冲区将保留 SSVARIANT 结构。<br /><br /> VARIANT_FALSE：列类型作为 DBTYPE_VARIANT 返回，且缓冲区将具有 VARIANT 结构。|  
  
## <a name="see-also"></a>请参阅  
 [数据类型&#40;OLE DB&#41;](data-types-ole-db.md)  
  
  