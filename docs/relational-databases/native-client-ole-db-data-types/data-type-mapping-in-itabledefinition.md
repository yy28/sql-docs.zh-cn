---
title: ITableDefinition 中的数据类型映射 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d3e828efa513db1ace272e59379f77d063220290
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297003"
---
# <a name="data-type-mapping-in-itabledefinition"></a>ITableDefinition 中的数据类型映射
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  使用**ITable 定义：创建表**函数创建表时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序使用者可以在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]传递的 DBCOLUMNDESC 数组的*pwszTypeName*成员中指定数据类型。 如果使用者按照名称指定列的数据类型，则忽略由 DBCOLUMNDESC 结构的 wType 成员表示的 OLE DB 数据类型映射**。  
  
 使用 DBCOLUMN DB 数据类型使用 DBCOLUMN DB 结构*wType*成员指定新的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]列数据类型时，本机客户端 OLE DB 提供程序将 OLE DB 数据类型映射如下。  
  
|OLE DB 数据类型|SQL Server<br /><br /> 数据类型|其他信息|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**位**||  
|DBTYPE_BYTES|binary、varbinary、image 或 varbinary(max)****************|本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序检查 DBCOLUMNDESC 结构的*ulColumnSize*成员。 根据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的值和版本，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序将类型映射到**映像**。<br /><br /> 如果*ulColumnSize*的值小于**二进制**数据类型列的最大长度，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序将检查 DBCOLUMNDESC *rgPropertySet*成员。 如果DBPROP_COL_FIXEDLENGTHVARIANT_TRUE，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序将类型映射到**二进制**。 如果属性的值VARIANT_FALSE，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序将类型映射到**varbinary**。 在这两种情况下，DBCOLUMNDESC 的 ulColumnSize 成员将确定创建的 SQL Server 列的宽度**。|  
|DBTYPE_CY|**钱**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**小林特**||  
|DBTYPE_I4|**Int**||  
|DBTYPE_NUMERIC|**数字**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序检查 DBCOLUMDESC *bPrecision*和*bScale*成员，以确定**数字**列的精度和比例。|  
|DBTYPE_R4|**真正**||  
|DBTYPE_R8|**浮动**||  
|DBTYPE_STR|char、varchar、text 或 varchar(max)****************|本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序检查 DBCOLUMNDESC 结构的*ulColumnSize*成员。 根据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的值和版本，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序将类型映射到**文本**。<br /><br /> 如果*ulColumnSize*的值小于多字节字符数据类型列的最大长度，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序将检查 DBCOLUMNDESC *rgPropertySet*成员。 如果DBPROP_COL_FIXEDLENGTHVARIANT_TRUE，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序将类型映射到**字符**。 如果属性的值为VARIANT_FALSE，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序将类型映射到**varchar**。 在这两种情况下，DBCOLUMNDESC ulColumnSize 成员将确定创建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列的宽度**。|  
|DBTYPE_UDT|**Udt**|需要 UDT 列时，ITableDefinition::CreateTable 将在 DBCOLUMNDESC 结构中用到以下信息********：<br /><br /> pwSzTypeName** 将被忽略。<br /><br /> rgPropertySets** 必须包括 DBPROPSET_SQLSERVERCOLUMN**** 属性集，如[使用用户定义的类型](../../relational-databases/native-client/features/using-user-defined-types.md)中的 DBPROPSET_SQLSERVERCOLUMN**** 部分所述。|  
|DBTYPE_UI1|**小金特**||  
|DBTYPE_WSTR|nchar、nvarchar、ntext 或 nvarchar(max)****************|本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序检查 DBCOLUMNDESC 结构的*ulColumnSize*成员。 基于该值，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序将类型映射到**ntext**。<br /><br /> 如果*ulColumnSize*的值小于 Unicode 字符数据类型列的最大长度，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序将检查 DBCOLUMNDESC *rgPropertySet*成员。 如果VARIANT_TRUEDBPROP_COL_FIXEDLENGTH，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序将类型映射到**nchar**。 如果属性的值VARIANT_FALSE，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序将类型映射到**nvarchar**。 在这两种情况下，DBCOLUMNDESC ulColumnSize 成员将确定创建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列的宽度**。|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  创建新表时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口只映射前一个表中指定的 OLE DB 数据类型枚举值。 尝试创建其中某一列为任何其他 OLE DB 数据类型的表时将生成错误。  
  
## <a name="see-also"></a>另请参阅  
 [数据类型 (OLE DB)](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
