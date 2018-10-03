---
title: DISCOVER_LOCATIONS 行集 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 6d3a1171-8e4d-4022-ade0-b785cf795d70
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5cec9ee5fc3b7dab0f8b2048b29d081e0971ee37
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106667"
---
# <a name="discoverlocations-rowset"></a>DISCOVER_LOCATIONS 行集
  返回有关备份文件的内容的信息。 您必须有权访问备份文件位置。  
  
## <a name="rowset-columns"></a>行集列  
 `DISCOVER_LOCATIONS`行集包含以下列。  
  
|列名|类型指示符|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|`LOCATION_BACKUP_FILE_PATHNAME`|`DBTYPE_WSTR`|必需，见下文。|备份文件的位置。|  
|`LOCATION_PARTITION_OBJECTPATH`|`DBTYPE_WSTR`||相对于数据文件夹的分区路径。|  
|`LOCATION_PARTITION_DATASOURCEID`|`DBTYPE_WSTR`||用于处理分区的数据源 ID。|  
|`LOCATION_PARTITION_DATASOURCENAME`|`DBTYPE_WSTR`||用于处理的数据源的名称。|  
|`LOCATION_PARTITION_NAME`|`DBTYPE_WSTR`||分区名称。|  
|`LOCATION_PARTITION_SIZE`|`DBTYPE_WSTR`||分区的近似大小。|  
|`LOCATION_CONNECTION_STRING`|`DBTYPE_WSTR`||处理中使用的数据源的连接字符串。|  
|`LOCATION_PARTITION_FOLDER`|`DBTYPE_WSTR`||生成备份文件时此分区的原始位置。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 `DISCOVER_LOCATIONS`行集可以限制下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`LOCATION_BACKUP_FILE_PATHNAME`|`DBTYPE_WSTR`|Required|  
|`LOCATION_PASSWORD PF_DBTYPE`|`DBTYPE_WSTR`|在备份过程中指定了该项时是必需的。 此限制不用来限制返回的行， 而用于提供访问该位置所需的密码。|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|ReplTest1|  
|--------------|-----------|  
|GUID|a07ccd92-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|位置|  
  
## <a name="see-also"></a>请参阅  
 [XML for Analysis 架构行集](xml-for-analysis-schema-rowsets.md)  
  
  
