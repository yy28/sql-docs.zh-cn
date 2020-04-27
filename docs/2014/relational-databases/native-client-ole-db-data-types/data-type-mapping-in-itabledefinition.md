---
title: ITableDefinition 中的数据类型映射 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e561742406c173b69bfb5040c2f2f51efdf5ed64
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63201218"
---
# <a name="data-type-mapping-in-itabledefinition"></a>ITableDefinition 中的数据类型映射
  使用**ITableDefinition：： CreateTable**函数创建表时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者可以在传递的 DBCOLUMNDESC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数组的*pwszTypeName*成员中指定数据类型。 如果使用者按照名称指定列的数据类型，则忽略由 DBCOLUMNDESC 结构的 wType 成员表示的 OLE DB 数据类型映射**。  
  
 使用 DBCOLUMNDESC 结构*wType*成员指定具有 OLE DB 数据类型的新列数据类型时，Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 提供程序将按如下所示映射 OLE DB 数据类型。  
  
|OLE DB 数据类型|SQL Server<br /><br /> 数据类型|其他信息|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|binary、varbinary、image 或 varbinary(max)****************|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序检查 DBCOLUMNDESC 结构的*ulColumnSize*成员。 基于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的值和版本， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将该类型映射到**映像**。<br /><br /> 如果*ulColumnSize*的值小于**binary**数据类型列的最大长度，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT OLE DB 提供程序将检查 DBCOLUMNDESC *rgPropertySets*成员。 如果 VARIANT_TRUE DBPROP_COL_FIXEDLENGTH，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将该类型映射为**binary**。 如果 VARIANT_FALSE 属性的值，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将该类型映射为**varbinary**。 在这两种情况下，DBCOLUMNDESC 的 ulColumnSize 成员将确定创建的 SQL Server 列的宽度**。|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**numeric**|Native Client OLE DB 提供程序检查 DBCOLUMDESC *bPrecision*和*bScale*成员，以确定数值列的精度和小数位数。 **numeric** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|char、varchar、text 或 varchar(max)****************|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序检查 DBCOLUMNDESC 结构的*ulColumnSize*成员。 基于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的值和版本， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将该类型映射为**文本**。<br /><br /> 如果*ulColumnSize*的值小于多字节字符数据类型列的最大长度，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将检查 DBCOLUMNDESC *rgPropertySets*成员。 如果 VARIANT_TRUE DBPROP_COL_FIXEDLENGTH，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将该类型映射为**char**。 如果 VARIANT_FALSE 属性的值，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将该类型映射为**varchar**。 在这两种情况下，DBCOLUMNDESC ulColumnSize 成员将确定创建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列的宽度**。|  
|DBTYPE_UDT|**UDT**|当需要 UDT 列时， `DBCOLUMNDESC`可以在结构中通过**ITableDefinition：： CreateTable**使用以下信息：<br /><br /> -   将忽略*pwSzTypeName* 。<br />-   *rgPropertySets*必须包括`DBPROPSET_SQLSERVERCOLUMN` [使用用户定义的类型](../native-client/features/using-user-defined-types.md)中的部分`DBPROPSET_SQLSERVERCOLUMN`中所述的属性集。|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|nchar、nvarchar、ntext 或 nvarchar(max)****************|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序检查 DBCOLUMNDESC 结构的*ulColumnSize*成员。 根据值， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将该类型映射为**ntext**。<br /><br /> 如果*ulColumnSize*的值小于 Unicode 字符数据类型列的最大长度，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将检查 DBCOLUMNDESC *rgPropertySets*成员。 如果 VARIANT_TRUE DBPROP_COL_FIXEDLENGTH，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将该类型映射为**nchar**。 如果 VARIANT_FALSE 属性的值，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将该类型映射到**nvarchar**。 在这两种情况下，DBCOLUMNDESC ulColumnSize 成员将确定创建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列的宽度**。|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  创建新表时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口只映射前一个表中指定的 OLE DB 数据类型枚举值。 尝试创建其中某一列为任何其他 OLE DB 数据类型的表时将生成错误。  
  
## <a name="see-also"></a>另请参阅  
 [数据类型 (OLE DB)](data-types-ole-db.md)  
  
  
