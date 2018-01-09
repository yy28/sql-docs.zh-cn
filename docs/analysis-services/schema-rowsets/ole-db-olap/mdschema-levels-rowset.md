---
title: "MDSCHEMA_LEVELS 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MDSCHEMA_LEVELS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_LEVELS rowset
ms.assetid: 4313e268-33f4-4e99-96d7-2ec26775c580
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7eb78b431b77dadfe216db5e30e77e9d5722b2a8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="mdschemalevels-rowset"></a>MDSCHEMA_LEVELS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]描述特定层次结构中的每个级别。  
  
## <a name="rowset-columns"></a>行集列  
 **MDSCHEMA_LEVELS**行集包含以下各列。  
  
|列名|类型指示符|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|此级别所属目录的名称。 **NULL**如果提供程序不支持目录。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|此级别所属的架构的名称。 **NULL**如果提供程序不支持架构。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|此级别所属多维数据集的名称。|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|此级别所属维度的唯一名称。 对于通过限定生成唯一名称的访问接口，此名称的各组成部分之间用分隔符分隔。|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|层次结构的唯一名称。 如果级别属于多个层次结构，则级别所属的每个层次结构都有对应的一行。 对于通过限定生成唯一名称的访问接口，此名称的各组成部分之间用分隔符分隔。|  
|**LEVEL_NAME**|**DBTYPE_WSTR**|级别的名称。|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|级别的正确转义的唯一名称。|  
|**LEVEL_GUID**|**DBTYPE_GUID**|不提供支持。|  
|**LEVEL_CAPTION**|**DBTYPE_WSTR**|与层次结构关联的标签或标题。 主要用于显示目的。 如果标题不存在， **LEVEL_NAME**返回。|  
|**LEVEL_NUMBER**|**DBTYPE_UI4**|级别距层次结构的根的距离。 根级别为零 (**0)**。|  
|**LEVEL_CARDINALITY**|**DBTYPE_UI4**|级别中的成员数。|  
|**LEVEL_TYPE**|**DBTYPE_I4**|级别类型：<br /><br /> **MDLEVEL_TYPE_GEO_CONTINENT** (**0x2001**)<br /><br /> **MDLEVEL_TYPE_GEO_REGION** (**0x2002**)<br /><br /> **MDLEVEL_TYPE_GEO_COUNTRY** (**0x2003**)<br /><br /> **MDLEVEL_TYPE_GEO_STATE_OR_PROVINCE** (**0x2004**)<br /><br /> **MDLEVEL_TYPE_GEO_COUNTY** (**0x2005**)<br /><br /> **MDLEVEL_TYPE_GEO_CITY** (**0x2006**)<br /><br /> **MDLEVEL_TYPE_GEO_POSTALCODE** (**0x2007**)<br /><br /> **MDLEVEL_TYPE_GEO_POINT** (**0x2008**)<br /><br /> **MDLEVEL_TYPE_ORG_UNIT** (**0x1011**)<br /><br /> **MDLEVEL_TYPE_BOM_RESOURCE** (**0x1012**)<br /><br /> **MDLEVEL_TYPE_QUANTITATIVE** (**0x1013**)<br /><br /> **MDLEVEL_TYPE_ACCOUNT** (**0x1014**)<br /><br /> **MDLEVEL_TYPE_CUSTOMER** (**0x1021**)<br /><br /> **MDLEVEL_TYPE_CUSTOMER_GROUP** (**0x1022**)<br /><br /> **MDLEVEL_TYPE_CUSTOMER_HOUSEHOLD** (**0x1023**)<br /><br /> **MDLEVEL_TYPE_PRODUCT** (**0x1031**)<br /><br /> **MDLEVEL_TYPE_PRODUCT_GROUP** (**0x1032**)<br /><br /> **MDLEVEL_TYPE_SCENARIO** (**0x1015**)<br /><br /> **MDLEVEL_TYPE_UTILITY** (**0x1016**)<br /><br /> **MDLEVEL_TYPE_PERSON** (**0x1041**)<br /><br /> **MDLEVEL_TYPE_COMPANY** (**0x1042**)<br /><br /> **MDLEVEL_TYPE_CURRENCY_SOURCE** (**0x1051**)<br /><br /> **MDLEVEL_TYPE_CURRENCY_DESTINATION** (**0x1052**)<br /><br /> **MDLEVEL_TYPE_CHANNEL** (**0x1061**)<br /><br /> **MDLEVEL_TYPE_REPRESENTATIVE** (**0x1062**)<br /><br /> **MDLEVEL_TYPE_PROMOTION** (**0x1071**)|  
|**DESCRIPTION**|**DBTYPE_WSTR**|用户可以阅读的级别说明。 如果不存在说明，则为 NULL。|  
|**CUSTOM_ROLLUP_SETTINGS**|**DBTYPE_I4**|指定自定义汇总选项的位图：<br /><br /> **MDLEVELS_CUSTOM_ROLLUP_EXPRESSION** (**0x01**) 指示表达式存在针对为此级别。 （不推荐使用）<br /><br /> **MDLEVELS_CUSTOM_ROLLUP_COLUMN** (**0x02**) 指示此级别的自定义汇总列。<br /><br /> **MDLEVELS_SKIPPED_LEVELS** (**0x04，则**) 指示与此级别的成员关联的已跳过的级别。<br /><br /> **MDLEVELS_CUSTOM_MEMBER_PROPERTIES** (**0x08**) 指示该级别成员具有自定义成员属性。<br /><br /> **MDLEVELS_UNARY_OPERATOR** (**0x10**) 指示在级别的成员具有一元运算符。|  
|**LEVEL_UNIQUE_SETTINGS**|**DBTYPE_I4**|如果级别只包含具有唯一名称或键的成员，则为指定包含唯一值的列的位图。 Msmd.h 文件为此位图定义以下位值常量：<br /><br /> **MDDIMENSIONS_MEMBER_KEY_UNIQUE** (**1**)<br /><br /> **MDDIMENSIONS_MEMBER_NAME_UNIQUE** (**2**)<br /><br /> <br /><br /> 请注意，密钥是始终在中唯一[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 该名称将是唯一的属性上设置是否**UniqueInDimension**或**UniqueInAttribute**|  
|**LEVEL_IS_VISIBLE**|**DBTYPE_BOOL**|指示级别是否可见的布尔值。<br /><br /> 始终返回 True。 如果相应级别不可见，则架构行集中将不包含该级别。|  
|**LEVEL_ORDERING_PROPERTY**|**DBTYPE_WSTR**|级别按其进行排序的属性的 ID。|  
|**LEVEL_DBTYPE**|**DBTYPE_I4**|**DBTYPE**枚举用于级别属性的成员键列。<br /><br /> 如果将串联键用作成员键列，则为 Null。|  
|**LEVEL_MASTER_UNIQUE_NAME**|**DBTYPE_WSTR**|始终返回 NULL。|  
|**LEVEL_NAME_SQL_COLUMN_NAME**|**DBTYPE_WSTR**|级别成员名称的 SQL 表示形式。|  
|**LEVEL_KEY_SQL_COLUMN_NAME**|**DBTYPE_WSTR**|级别成员键值的 SQL 表示形式。|  
|**LEVEL_UNIQUE_NAME_SQL_COLUMN_NAME**|**DBTYPE_WSTR**|成员唯一名称的 SQL 表示形式。|  
|**LEVEL_ATTRIBUTE_HIERARCHY_NAME**|**DBTYPE_WSTR**|提供级别来源的属性层次结构的名称。|  
|**LEVEL_KEY_CARDINALITY**|**DBTYPE_UI2**|级别键中的列的数量。|  
|**LEVEL_ORIGIN**|**DBTYPE_UI2**|定义如何确定级别来源的位图：<br /><br /> **MD_ORIGIN_USER_DEFINED**标识用户定义层次结构中的级别。<br /><br /> **MD_ORIGIN_ATTRIBUTE**标识属性层次结构中的级别。<br /><br /> **MD_ORIGIN_KEY_ATTRIBUTE**标识键属性层次结构中的级别。<br /><br /> **MD_ORIGIN_INTERNAL**标识未启用属性层次结构中的级别。|  
  
 行集按排序**CATALOG_NAME**， **SCHEMA_NAME**， **CUBE_NAME**， **DIMENSION_UNIQUE_NAME**， **HIERARCHY_UNIQUE_NAME**， **LEVEL_NUMBER**。  
  
## <a name="restriction-columns"></a>限制列  
 **MDSCHEMA_LEVELS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|可选。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|可选。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|可选。|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|可选。|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|可选。|  
|**LEVEL_NAME**|**DBTYPE_WSTR**|可选。|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|可选。|  
|**LEVEL_ORIGIN**|**DBTYPE_UI2**|（可选）默认限制是实际上在**MD_USER_DEFINED**和**MD_SYSTEM_ENABLED**|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|（可选）默认限制是值为 1。 位图，并使用以下有效的值之一：<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
|**LEVEL_VISIBILITY**|**DBTYPE_UI2**|（可选）默认限制是值为 1。 位图，并使用以下值之一：<br /><br /> 1 可见<br /><br /> 2 不可见|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB for OLAP 架构行集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
