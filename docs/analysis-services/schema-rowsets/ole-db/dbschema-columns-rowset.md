---
title: DBSCHEMA_COLUMNS 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2bb1fec6a1633f545f0c65feda93c7e19c649a6e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="dbschemacolumns-rowset"></a>DBSCHEMA_COLUMNS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  提供满足给定限制条件的所有列的列信息。  
  
## <a name="rowset-columns"></a>行集列  
 **DBSCHEMA_COLUMNS**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**TABLE_CATALOG**|**DBTYPE_WSTR**||数据库的名称。|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**||不提供支持。|  
|**TABLE_NAME**|**DBTYPE_WSTR**||多维数据集的名称。|  
|**COLUMN_NAME**|**DBTYPE_WSTR**||属性层次结构或度量值的名称。|  
|**COLUMN_GUID**|**DBTYPE_GUID**||不提供支持。|  
|**COLUMN_PROPID**|**DBTYPE_UI4**||不提供支持。|  
|**ORDINAL_POSITION**|**DBTYPE_UI4**||列的位置，从 1 开始。|  
|**COLUMN_HAS_DEFAULT**|**DBTYPE_BOOL**||不提供支持。|  
|**COLUMN_DEFAULT**|**DBTYPE_WSTR**||不提供支持。|  
|**COLUMN_FLAGS**|**DBTYPE_UI4**||A **DBCOLUMNFLAGS**位掩码，该值指示列属性。 请参阅中的 DBCOLUMNFLAGS 枚举类型[IColumnsInfo::GetColumnInfo](http://msdn2.microsoft.com/library/ms722704.aspx)|  
|**IS_NULLABLE**|**DBTYPE_BOOL**||始终返回**false**。|  
|**DATA_TYPE**|**DBTYPE_WSTR**<br /><br /> **DBTYPE_VARIANT**||列的数据类型。 返回维度列的字符串和度量值的变量。|  
|**TYPE_GUID**|**DBTYPE_GUID**||不提供支持。|  
|**CHARACTER_MAXIMUM_LENGTH**|**DBTYPE_UI4**||列中值的最大可能长度。<br /><br /> 这从**DataSize**中的属性**DataItem**。|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**||字符或二进制值列中的值的最大可能长度（字节）。<br /><br /> 值为零 (0) 指示该列没有最大长度。<br /><br /> **NULL**将返回为不返回二进制或字符数据类型的列。|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**||对于数值数据列的最大精度类型以外**DBTYPE_VARNUMERIC**。|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||小数点右侧的数字个数**DBTYPE_DECIMAL**， **DBTYPE_NUMERIC**， **DBTYPE_VARNUMERIC**。 否则，这就是**NULL**。|  
|**DATETIME_PRECISION**|**DBTYPE_UI4**||不提供支持。|  
|**CHARACTER_SET_CATALOG**|**DBTYPE_WSTR**||不提供支持。|  
|**CHARACTER_SET_SCHEMA**|**DBTYPE_WSTR**||不提供支持。|  
|**CHARACTER_SET_NAME**|**DBTYPE_WSTR**||不提供支持。|  
|**COLLATION_CATALOG**|**DBTYPE_WSTR**||不提供支持。|  
|**COLLATION_SCHEMA**|**DBTYPE_WSTR**||不提供支持。|  
|**COLLATION_NAME**|**DBTYPE_WSTR**||不提供支持。|  
|**DOMAIN_CATALOG**|**DBTYPE_WSTR**||不提供支持。|  
|**DOMAIN_SCHEMA**|**DBTYPE_WSTR**||不提供支持。|  
|**A I N _**|**DBTYPE_WSTR**||不提供支持。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||不提供支持。|  
|**COLUMN_OLAP_TYPE**|**DBTYPE_WSTR**||对象的 OLAP 类型。<br /><br /> **度量值**指示对象是度量值。<br /><br /> **属性**指示对象是维度属性。<br /><br /> **架构**指示对象是架构中的列。|  
  
 行集按排序**TABLE_CATALOG**， **TABLE_SCHEMA**， **TABLE_NAME**。  
  
## <a name="restriction-columns"></a>限制列  
 **DBSCHEMA_COLUMNS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**TABLE_CATALOG**|**DBTYPE_WSTR**|選擇性|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**|選擇性|  
|**TABLE_NAME**|**DBTYPE_WSTR**|選擇性|  
|**COLUMN_NAME**|**DBTYPE_WSTR**|選擇性|  
|**COLUMN_OLAP_TYPE**|**DBTYPE_WSTR**|選擇性|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB 架构行集合](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  
