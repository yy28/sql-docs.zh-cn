---
title: DISCOVER_STORAGE_TABLE_COLUMNS 行集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 24abb88e-33a9-4ae2-829d-cdef0ff22ec1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 240230784860e9484ebc03ba6740eaf5d56387fa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48089067"
---
# <a name="discoverstoragetablecolumns-rowset"></a>DISCOVER_STORAGE_TABLE_COLUMNS 行集
  在列级提供有关在 SharePoint 或表格模式下运行的 Analysis Services 数据库使用的存储表的信息。  
  
 **适用于：** 表格模型  
  
## <a name="rowset-columns"></a>行集列  
 `DISCOVER_STORAGE_TABLE_COLUMNS`行集包含以下列。  
  
|**列名**|**类型指示符**|**限制**|**Description**|  
|---------------------|------------------------|---------------------|---------------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|用户帐户控制|指定包含表的数据库名称。 如果省略，则使用当前数据库。<br /><br /> `DISCOVER_STORAGE_TABLE_COLUMNS`行集，可通过使用此列进行限制。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|用户帐户控制|指定包含表的多维数据集或模型。<br /><br /> `DISCOVER_STORAGE_TABLES`行集，可通过使用此列进行限制。|  
|`MEASURE_GROUP_NAME`|`DBTYPE_WSTR`|用户帐户控制|度量值组的名称。|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`||维度的名称。|  
|`ATTRIBUTE_NAME`|`DBTYPE_WSTR`||该属性的名称。|  
|`TABLE_ID`|`DBTYPE_WSTR`||表的 ID。|  
|`COLUMN_ID`|`DBTYPE_ WSTR`||列的 ID。 该列 ID 在 xVelocity 内存中分析引擎 (VertiPaq) 的内部使用并且仅供参考。|  
|`COLUMN_TYPE`|`DBTYPE_WSTR`||列的类型。 该列类型在 xVelocity 内存中分析引擎 (VertiPaq) 的内部使用并且仅供参考。<br /><br /> -BASIC_DATA<br />-HIERARCHY_DATAID_TO_POSITION<br />-HIERARCHY_POSITION_TO_DATAID<br />-关系|  
|`COLUMN_ENCODING`|`DBTYPE_UI8`||表示用于列数据的编码类型的整数。<br /><br /> -   **0**，用于`COLUMN_TYPE`: HIERARCHY_DATAID_TO_POSITION、 HIERARCHY_POSITION_TO_DATAID、 关系<br />-   **1**，用于`COLUMN_TYPE`: BASIC_DATA<br />-   **2**，用于`COLUMN_TYPE`: BASIC_DATA|  
|`DATATYPE`|`DBTYPE_WSTR`||列的数据类型。 具有以下可能值：<br /><br /> -DBTYPE_BOOL<br />-DBTYPE_CY<br />-DBTYPE_DATE<br />-DBTYPE_I4<br />-DBTYPE_I8<br />-DBTYPE_R8<br />-DBTYPE_WSTR<br />-不适用|  
|`ISKEY`|`DBTYPE_BOOL`||如果列用作主键或外键，则为 `True`；否则为 `false`。|  
|`ISUNIQUE`|`DBTYPE_BOOL`||`True` 如果列中的值是唯一的;否则为`false`。|  
|`ISNULLABLE`|`DBTYPE_BOOL`||如果列是可为 Null 的，则为 `True`；否则为 `false`。|  
|`ISROWNUMBER`|`DBTYPE_BOOL`||如果列是行号列，则为 `True`。 行号列供 xVelocity 内存中分析引擎内部使用。|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|ReplTest1|  
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
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 架构行集](../analysis-services-schema-rowsets.md)  
  
  
