---
title: "DISCOVER_STORAGE_TABLE_COLUMNS 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 24abb88e-33a9-4ae2-829d-cdef0ff22ec1
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 126a0f1c261cc13f5a3673a67c87d12aac5faece
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="discoverstoragetablecolumns-rowset"></a>DISCOVER_STORAGE_TABLE_COLUMNS 行集
  在列级提供有关在 SharePoint 或表格模式下运行的 Analysis Services 数据库使用的存储表的信息。  
  
 **适用于：** 表格模型  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_STORAGE_TABLE_COLUMNS**行集包含以下各列。  
  
|**列名**|**类型指示符**|**限制**|**Description**|  
|---------------------|------------------------|---------------------|---------------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|是|指定包含表的数据库名称。 如果省略，则使用当前数据库。<br /><br /> **DISCOVER_STORAGE_TABLE_COLUMNS**行集可通过使用此列来限制。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|是|指定包含表的多维数据集或模型。<br /><br /> **DISCOVER_STORAGE_TABLES**行集可通过使用此列来限制。|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|是|度量值组的名称。|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||维度的名称。|  
|**ATTRIBUTE_NAME**|**DBTYPE_WSTR**||属性的名称。|  
|**针对 TABLE_ID 所**|**DBTYPE_WSTR**||表的 ID。|  
|**COLUMN_ID**|**DBTYPE_ WSTR**||列的 ID。 该列 ID 在 xVelocity 内存中分析引擎 (VertiPaq) 的内部使用并且仅供参考。|  
|**COLUMN_TYPE**|**DBTYPE_WSTR**||列的类型。 该列类型在 xVelocity 内存中分析引擎 (VertiPaq) 的内部使用并且仅供参考。<br /><br /> BASIC_DATA<br /><br /> HIERARCHY_DATAID_TO_POSITION<br /><br /> HIERARCHY_POSITION_TO_DATAID<br /><br /> RELATIONSHIP|  
|**COLUMN_ENCODING**|**DBTYPE_UI8**||表示用于列数据的编码类型的整数。<br /><br /> **0**、 用于**COLUMN_TYPE**: HIERARCHY_DATAID_TO_POSITION，HIERARCHY_POSITION_TO_DATAID，关系<br /><br /> **1**、 用于**COLUMN_TYPE**: BASIC_DATA<br /><br /> **2**、 用于**COLUMN_TYPE**: BASIC_DATA|  
|**数据类型**|**DBTYPE_WSTR**||列的数据类型。 具有以下可能值：<br /><br /> DBTYPE_BOOL<br /><br /> DBTYPE_CY<br /><br /> DBTYPE_DATE<br /><br /> DBTYPE_I4<br /><br /> DBTYPE_I8<br /><br /> DBTYPE_R8<br /><br /> DBTYPE_WSTR<br /><br /> N/A|  
|**ISKEY**|**DBTYPE_BOOL**||**True**如果列是主键或外键类型用作; 否则为**false**。|  
|**是唯一的**|**DBTYPE_BOOL**||**True**列中的值是否唯一; 否则为**false**。|  
|**ISNULLABLE**|**DBTYPE_BOOL**||**True**此列是否可以为 null; 否则为**false**。|  
|**ISROWNUMBER**|**DBTYPE_BOOL**||**True**如果列是行号列。 行号列供 xVelocity 内存中分析引擎内部使用。|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|值|  
|--------------|-----------|  
|GUID|a07ccd44-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|StorageTableColumns|  
  
## <a name="example"></a>示例  
 以下代码示例使用 DMV 查询返回结果集。  
  
```  
SELECT *  
FROM $System.DISCOVER_STORAGE_TABLE_COLUMNS  
ORDER BY TABLE_ID DESC  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 架构行集](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
