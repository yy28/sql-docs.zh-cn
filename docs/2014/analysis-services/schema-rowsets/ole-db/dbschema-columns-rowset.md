---
title: DBSCHEMA_COLUMNS 行集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DBSCHEMA_COLUMNS
topic_type:
- apiref
helpviewer_keywords:
- DBSCHEMA_COLUMNS rowset
ms.assetid: 653bdd07-a533-4a99-8b6a-6e5c7322e1f3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6354f098140ff7775967fad89b1198e18619395b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48173187"
---
# <a name="dbschemacolumns-rowset"></a>DBSCHEMA_COLUMNS 行集
  提供满足给定限制条件的所有列的列信息。  
  
## <a name="rowset-columns"></a>行集列  
 `DBSCHEMA_COLUMNS`行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`||数据库的名称。|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`||不提供支持。|  
|`TABLE_NAME`|`DBTYPE_WSTR`||多维数据集的名称。|  
|`COLUMN_NAME`|`DBTYPE_WSTR`||属性层次结构或度量值的名称。|  
|`COLUMN_GUID`|`DBTYPE_GUID`||不提供支持。|  
|`COLUMN_PROPID`|`DBTYPE_UI4`||不提供支持。|  
|`ORDINAL_POSITION`|`DBTYPE_UI4`||列的位置，从 1 开始。|  
|`COLUMN_HAS_DEFAULT`|`DBTYPE_BOOL`||不提供支持。|  
|`COLUMN_DEFAULT`|`DBTYPE_WSTR`||不提供支持。|  
|`COLUMN_FLAGS`|`DBTYPE_UI4`||指示列属性的 `DBCOLUMNFLAGS` 位掩码。 请参阅中的 DBCOLUMNFLAGS 枚举类型[icolumnsinfo:: Getcolumninfo](http://msdn2.microsoft.com/library/ms722704.aspx)|  
|`IS_NULLABLE`|`DBTYPE_BOOL`||始终返回`false`。|  
|`DATA_TYPE`|`DBTYPE_WSTR`<br /><br /> `DBTYPE_VARIANT`||列的数据类型。 返回维度列的字符串和度量值的变量。|  
|`TYPE_GUID`|`DBTYPE_GUID`||不提供支持。|  
|`CHARACTER_MAXIMUM_LENGTH`|`DBTYPE_UI4`||列中值的最大可能长度。<br /><br /> 可从 `DataSize` 中的 `DataItem` 属性检索此值。|  
|`CHARACTER_OCTET_LENGTH`|`DBTYPE_UI4`||字符或二进制值列中的值的最大可能长度（字节）。<br /><br /> 值为零 (0) 指示该列没有最大长度。<br /><br /> 对于不返回二进制或字符数据类型的列，将返回 `NULL`。|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||非 `DBTYPE_VARNUMERIC` 的数值数据类型列的最大精度。|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||`DBTYPE_DECIMAL`、`DBTYPE_NUMERIC`、`DBTYPE_VARNUMERIC` 的小数点右侧的位数。 否则，这就是`NULL`。|  
|`DATETIME_PRECISION`|`DBTYPE_UI4`||不提供支持。|  
|`CHARACTER_SET_CATALOG`|`DBTYPE_WSTR`||不提供支持。|  
|`CHARACTER_SET_SCHEMA`|`DBTYPE_WSTR`||不提供支持。|  
|`CHARACTER_SET_NAME`|`DBTYPE_WSTR`||不提供支持。|  
|`COLLATION_CATALOG`|`DBTYPE_WSTR`||不提供支持。|  
|`COLLATION_SCHEMA`|`DBTYPE_WSTR`||不提供支持。|  
|`COLLATION_NAME`|`DBTYPE_WSTR`||不提供支持。|  
|`DOMAIN_CATALOG`|`DBTYPE_WSTR`||不提供支持。|  
|`DOMAIN_SCHEMA`|`DBTYPE_WSTR`||不提供支持。|  
|`DOMAIN_NAME`|`DBTYPE_WSTR`||不提供支持。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||不提供支持。|  
|`COLUMN_OLAP_TYPE`|`DBTYPE_WSTR`||对象的 OLAP 类型。<br /><br /> `MEASURE` 指示对象是一个度量值。<br /><br /> `ATTRIBUTE` 指示对象是一个维度属性。<br /><br /> `SCHEMA` 指示对象是架构中的列。|  
  
 行集按 `TABLE_CATALOG`、`TABLE_SCHEMA`、`TABLE_NAME` 排序。  
  
## <a name="restriction-columns"></a>限制列  
 `DBSCHEMA_COLUMNS`行集可以限制下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`|可选|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`|可选|  
|`TABLE_NAME`|`DBTYPE_WSTR`|可选|  
|`COLUMN_NAME`|`DBTYPE_WSTR`|可选|  
|`COLUMN_OLAP_TYPE`|`DBTYPE_WSTR`|可选|  
  
## <a name="see-also"></a>请参阅  
 [OLE DB 架构行集](ole-db-schema-rowsets.md)  
  
  
