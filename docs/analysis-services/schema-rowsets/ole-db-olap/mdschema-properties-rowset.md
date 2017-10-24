---
title: "MDSCHEMA_PROPERTIES 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MDSCHEMA_PROPERTIES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_PROPERTIES rowset
ms.assetid: 95c480f7-c525-44ba-a59b-cd36f5855a4f
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6f77505e9daa9efc330bfcd358a37982eace8935
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="mdschemaproperties-rowset"></a>MDSCHEMA_PROPERTIES 行集
  描述数据库中的成员的属性。  
  
## <a name="rowset-columns"></a>行集列  
 **MDSCHEMA_PROPERTIES**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||数据库的名称。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||此属性所属的架构的名称。 **NULL**如果提供程序不支持架构。|  
|**CUBE_NAME**|**DBTYPE_WSTR**||多维数据集的名称。|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**||维度的唯一名称。 对于通过限定生成唯一名称的访问接口，此名称的各组成部分之间用分隔符分隔。|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**||层次结构的唯一名称。 对于通过限定生成唯一名称的访问接口，此名称的各组成部分之间用分隔符分隔。|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**||此属性所属的级别的唯一名称。 如果提供程序不支持命名的级别，它应返回**DIMENSION_UNIQUE_NAME**为此字段的值。 对于通过限定生成唯一名称的访问接口，此名称的各组成部分之间用分隔符分隔。|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**||此属性所属的成员的唯一名称。 用于不支持命名级别或具有基于单个成员的属性的数据存储区。 如果该属性适用于级别中的所有成员，此列是**NULL**。 对于通过限定生成唯一名称的访问接口，此名称的各组成部分之间用分隔符分隔。|  
|**PROPERTY_TYPE**|**DBTYPE_I2**||用于指定属性类型的位图：<br /><br /> **MDPROP_MEMBER** (**1**) 标识的成员属性。 此属性可用于 SELECT 语句的 DIMENSION PROPERTIES 子句。<br /><br /> **MDPROP_CELL** (**2**) 标识的单元格的属性。 此属性可用于在 SELECT 语句结尾处出现的 CELL PROPERTIES 子句。<br /><br /> **MDPROP_SYSTEM** (**4**) 标识的内部属性。<br /><br /> **MDPROP_BLOB** (**8**) 标识一个属性，它包含二进制大型对象 (blob)。|  
|**PROPERTY_NAME**|**DBTYPE_WSTR**||属性的名称。 如果该属性的键是属性的名称相同**PROPERTY_NAME**将为空。|  
|**PROPERTY_CAPTION**|**DBTYPE_WSTR**||与属性关联的标签或标题，主要用于显示目的。 返回**PROPERTY_NAME**如果标题不存在。|  
|**DATA_TYPE**|**DBTYPE_UI2**||属性的数据类型。|  
|**CHARACTER_MAXIMUM_LENGTH**|**DBTYPE_UI4**||如果数据类型为 character、binary 或 bit，则为属性的最大长度。<br /><br /> 零表示未定义属性的最大长度。<br /><br /> 返回**NULL**对于所有其他数据类型。|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**||如果数据类型为 character 或 binary，则为属性的最大可能长度（字节）。<br /><br /> 零表示未定义属性的最大长度。<br /><br /> 返回**NULL**对于所有其他数据类型。|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**||如果数据类型为 numeric，则为属性的最大精度。<br /><br /> 返回**NULL**对于所有其他数据类型。|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||如果它是小数点右侧的数字个数**DBTYPE_NUMERIC**或**DBTYPE_DECIMAL**类型。<br /><br /> 返回**NULL**对于所有其他数据类型。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||易读的属性说明。 **NULL**如果没有任何其他说明存在。|  
|**PROPERTY_CONTENT_TYPE**|**DBTYPE_I2**||属性的类型。 可以为下列枚举之一：<br /><br /> **MD_PROPTYPE_REGULAR** (**0x00**)<br /><br /> **MD_PROPTYPE_ID** (**0x01**)<br /><br /> **MD_PROPTYPE_RELATION_TO_PARENT** (**0x02**)<br /><br /> **MD_PROPTYPE_ROLLUP_OPERATOR** (**0x03**)<br /><br /> **MD_PROPTYPE_ORG_TITLE** (**0x11**)<br /><br /> **MD_PROPTYPE_CAPTION** (**0x21**)<br /><br /> **MD_PROPTYPE_CAPTION_SHORT** (**0x22**)<br /><br /> **MD_PROPTYPE_CAPTION_DESCRIPTION** (**0x23**)<br /><br /> **MD_PROPTYPE_CAPTION_ABREVIATION** (**0x24**)<br /><br /> **MD_PROPTYPE_WEB_URL** (**0x31**)<br /><br /> **MD_PROPTYPE_WEB_HTML** (**0x32**)<br /><br /> **MD_PROPTYPE_WEB_XML_OR_XSL** (**0x33**)<br /><br /> **MD_PROPTYPE_WEB_MAIL_ALIAS** (**0x34**)<br /><br /> **MD_PROPTYPE_ADDRESS** (**0x41 向**)<br /><br /> **MD_PROPTYPE_ADDRESS_STREET** (**0x42**)<br /><br /> **MD_PROPTYPE_ADDRESS_HOUSE** (**0x43**)<br /><br /> **MD_PROPTYPE_ADDRESS_CITY** (**0x44**)<br /><br /> **MD_PROPTYPE_ADDRESS_STATE_OR_PROVINCE** (**0x45**)<br /><br /> **MD_PROPTYPE_ADDRESS_ZIP** (**0x46**)<br /><br /> **MD_PROPTYPE_ADDRESS_QUARTER** (**0x47**)<br /><br /> **MD_PROPTYPE_ADDRESS_COUNTRY** (**0x48**)<br /><br /> **MD_PROPTYPE_ADDRESS_BUILDING** (**0x49**)<br /><br /> **MD_PROPTYPE_ADDRESS_ROOM** (**0x4A**)<br /><br /> **MD_PROPTYPE_ADDRESS_FLOOR** (**0x4b 放**)<br /><br /> **MD_PROPTYPE_ADDRESS_FAX** (**0x4C**)<br /><br /> **MD_PROPTYPE_ADDRESS_PHONE** (**就将 0x4D**)<br /><br /> **MD_PROPTYPE_GEO_CENTROID_X** (**0x61**)<br /><br /> **MD_PROPTYPE_GEO_CENTROID_Y** (**0x62**)<br /><br /> **MD_PROPTYPE_GEO_CENTROID_Z** (**0x63**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_TOP** (**0x64**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_LEFT** (**0x65**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_BOTTOM** (**0x66**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_RIGHT** (**0x67**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_FRONT** (**0x68**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_REAR** (**0x69**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_POLYGON** (**0x6A**)<br /><br /> **MD_PROPTYPE_PHYSICAL_SIZE** (**0x71**)<br /><br /> **MD_PROPTYPE_PHYSICAL_COLOR** (**0x72**)<br /><br /> **MD_PROPTYPE_PHYSICAL_WEIGHT** (**0x73**)<br /><br /> **MD_PROPTYPE_PHYSICAL_HEIGHT** (**0x74**)<br /><br /> **MD_PROPTYPE_PHYSICAL_WIDTH** (**0x75**)<br /><br /> **MD_PROPTYPE_PHYSICAL_DEPTH** (**0x76**)<br /><br /> **MD_PROPTYPE_PHYSICAL_VOLUME** (**0x77**)<br /><br /> **MD_PROPTYPE_PHYSICAL_DENSITY** (**0x78**)<br /><br /> **MD_PROPTYPE_PERSON_FULL_NAME** (**0x82**)<br /><br /> **MD_PROPTYPE_PERSON_FIRST_NAME** (**0x83**)<br /><br /> **MD_PROPTYPE_PERSON_LAST_NAME** (**0x84**)<br /><br /> **MD_PROPTYPE_PERSON_MIDDLE_NAME** (**0x85**)<br /><br /> **MD_PROPTYPE_PERSON_DEMOGRAPHIC** (**0x86**)<br /><br /> **MD_PROPTYPE_PERSON_CONTACT** (**0x87**)<br /><br /> **MD_PROPTYPE_QTY_RANGE_LOW** (**0x91**)<br /><br /> **MD_PROPTYPE_QTY_RANGE_HIGH** (**0x92**)<br /><br /> **MD_PROPTYPE_FORMATTING_COLOR** (**0xA1**)<br /><br /> **MD_PROPTYPE_FORMATTING_ORDER** (**0xA2**)<br /><br /> **MD_PROPTYPE_FORMATTING_FONT** (**0xA3**)<br /><br /> **MD_PROPTYPE_FORMATTING_FONT_EFFECTS** (**0xA4**)<br /><br /> **MD_PROPTYPE_FORMATTING_FONT_SIZE** (**0xA5**)<br /><br /> **MD_PROPTYPE_FORMATTING_SUB_TOTAL** (**0xA6**)<br /><br /> **MD_PROPTYPE_DATE** (**0xB1**)<br /><br /> **MD_PROPTYPE_DATE_START** (**0xB2**)<br /><br /> **MD_PROPTYPE_DATE_ENDED** (**0xB3**)<br /><br /> **MD_PROPTYPE_DATE_CANCELED** (**0xB4**)<br /><br /> **MD_PROPTYPE_DATE_MODIFIED** (**0xB5**)<br /><br /> **MD_PROPTYPE_DATE_DURATION** (**0xB6**)<br /><br /> **MD_PROPTYPE_VERSION** (**0xC1**)|  
|**SQL_COLUMN_NAME**|**DBTYPE_WSTR**||多维数据集维度或数据库维度中的 SQL 查询中使用的属性的名称。|  
|**LANGUAGE**|**DBTYPE_UI2**||转换表示为**LCID**。 仅对属性翻译有效。|  
|**PROPERTY_ORIGIN**|**DBTYPE_UI2**||标识属性应用的层次结构的类型：<br /><br /> **MD_USER_DEFINED** (**1**) 指示该属性是用户定义层次结构上<br /><br /> **MD_SYSTEM_ENABLED** (**2**) 指示属性显示在属性层次结构<br /><br /> **MD_SYSTEM_DISABLED** (**4**) 指示属性显示在未启用属性层次结构。|  
|**PROPERTY_ATTRIBUTE_HIERARCHY_NAME**|**DBTYPE_WSTR**||确定此特性的属性层次结构的名称。|  
|**PROPERTY_CARDINALITY**|**DBTYPE_WSTR**||属性的基数。 可能的值包括下列字符串：<br /><br /> **其中一个**<br /><br /> **许多**|  
|**MIME_TYPE**|**DBTYPE_WSTR**||二进制大型对象 (BLOB) 的 MIME 类型。|  
|**PROPERTY_IS_VISIBLE**|**DBTYPE_BOOL**||指示属性是否可见的布尔值。<br /><br /> **TRUE**如果属性是可见的; 否则为**FALSE**。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 **MDSCHEMA_PROPERTIES**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|必需|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|可选|  
|**CUBE_NAME**|**DBTYPE_WSTR**|可选|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|可选|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|可选|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|可选|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**|可选|  
|**PROPERTY_TYPE**|**DBTYPE_I2**|可选|  
|**PROPERTY_NAME**|**DBTYPE_WSTR**|可选|  
|**PROPERTY_CONTENT_TYPE**|**DBTYPE_I2**|（可选）默认限制已到位上**MDPROP_MEMBER**或者**MDPROP_CELL**。|  
|**PROPERTY_ORIGIN**|**DBTYPE_UI2**|（可选）默认限制已到位上**MD_USER_DEFINED**或者**MD_SYSTEM_ENABLED**。|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|（可选）默认限制是值为 1。  位图，并使用以下有效的值之一：<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
|**PROPERTY_VISIBILITY**|**DBTYPE_UI2**|（可选）默认限制是值为 1。 位图，并使用以下有效的值之一：<br /><br /> 1 可见<br /><br /> 2 不可见|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB for OLAP 架构行集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

