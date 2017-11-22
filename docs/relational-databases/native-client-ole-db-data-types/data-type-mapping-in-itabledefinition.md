---
title: "数据类型映射中 ITableDefinition |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-data-types
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- SQL Server Native Client OLE DB provider, data types
- ITableDefinition interface
- DBCOLUMNDESC structure
- data types [OLE DB]
- CreateTable function
- OLE DB, data types
ms.assetid: 13292d1f-c17e-4d11-bf98-3460a10cbb18
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c9e8c3fbcce7146c2de17caa97e70a539de6a90b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="data-type-mapping-in-itabledefinition"></a>ITableDefinition 中的数据类型映射
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  通过使用创建表时**ITableDefinition::CreateTable**函数， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序使用者可以指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的数据类型*pwszTypeName*传递 DBCOLUMNDESC 数组的成员。 如果使用者按名称指定列的数据类型，OLE DB 数据类型映射，由表示*wType* DBCOLUMNDESC 结构中，成员将被忽略。  
  
 使用 DBCOLUMNDESC 结构的 OLE DB 数据类型指定新的列数据类型时*wType*成员， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将 OLE DB 数据类型的映射，如下所示。  
  
|OLE DB 数据类型|SQL Server<br /><br /> 数据类型|其他信息|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**二进制**， **varbinary**，**映像，**或**varbinary （max)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序检查*ulColumnSize* DBCOLUMNDESC 结构的成员。 基于的值和版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将映射到类型**映像**。<br /><br /> 如果值*ulColumnSize*小于的最大长度**二进制**数据类型列，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序检查 DBCOLUMNDESC *rgPropertySets*成员。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将映射到类型**二进制**。 如果属性的值是 VARIANT_FALSE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将映射到类型**varbinary**。 在任一情况下，DBCOLUMNDESC *ulColumnSize*成员确定创建的 SQL Server 列的宽度。|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**int**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**numeric**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序检查 DBCOLUMDESC *bPrecision*和*bScale*成员确定精度和扩展，从而**数值**列。|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**， **varchar**，**文本，**或**varchar （max)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序检查*ulColumnSize* DBCOLUMNDESC 结构的成员。 基于的值和版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将映射到类型**文本**。<br /><br /> 如果值*ulColumnSize*小于多字节字符数据类型列的最大长度则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序检查 DBCOLUMNDESC *rgPropertySets*成员。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将映射到类型**char**。 如果属性的值是 VARIANT_FALSE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将映射到类型**varchar**。 在任一情况下，DBCOLUMNDESC *ulColumnSize*成员确定的宽度[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]创建列。|  
|DBTYPE_UDT|**UDT**|在使用以下信息**DBCOLUMNDESC**结构通过**ITableDefinition::CreateTable**需要 UDT 列时：<br /><br /> *pwSzTypeName*将被忽略。<br /><br /> *rgPropertySets*必须包括**DBPROPSET_SQLSERVERCOLUMN**属性设置在上一部分中所述**DBPROPSET_SQLSERVERCOLUMN**中[使用用户定义类型](../../relational-databases/native-client/features/using-user-defined-types.md)。|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|**nchar**， **nvarchar**， **ntext**或**nvarchar (max)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序检查*ulColumnSize* DBCOLUMNDESC 结构的成员。 值， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将映射到类型**ntext**。<br /><br /> 如果值*ulColumnSize*小于最大长度的 Unicode 字符数据类型列，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序检查 DBCOLUMNDESC *rgPropertySets*成员。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将映射到类型**nchar**。 如果属性的值是 VARIANT_FALSE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将映射到类型**nvarchar**。 在任一情况下，DBCOLUMNDESC *ulColumnSize*成员确定的宽度[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]创建列。|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  创建新表时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口只映射前一个表中指定的 OLE DB 数据类型枚举值。 尝试创建其中某一列为任何其他 OLE DB 数据类型的表时将生成错误。  
  
## <a name="see-also"></a>另请参阅  
 [数据类型 &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
