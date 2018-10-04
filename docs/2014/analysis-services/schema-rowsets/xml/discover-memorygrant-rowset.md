---
title: DISCOVER_MEMORYGRANT 行集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: d254e42d-9918-47ce-b6df-47f1f0b432dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 21e24d1a7ab727eeb2c014870adb9928aed989dd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48154257"
---
# <a name="discovermemorygrant-rowset"></a>DISCOVER_MEMORYGRANT 行集
  返回由当前正在服务器上运行的作业占用的内部内存配额授予的列表。 若要查明作业是否在服务器上运行，请使用 `Select * from $System.Discover_Jobs`。  
  
 **适用于：** 表格模型和多维模型  
  
## <a name="rowset-columns"></a>行集列  
 `DISCOVER_MEMORYGRANT`行集包含以下列。  
  
|列名|类型指示符|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|`MEMORY_ID`|**DBTYPE_I8**||用于标识内存配额授予的数字。 在单个 DISCOVER_MEMORYGRANT 请求的上下文中是唯一的。|  
|`SPID`|`DBTYPE_I4`|Required|SPID，可通过运行 `Select * from $System.Discover_Sessions` 获得它。|  
|`CreationTime`|`DBTYPE_I8 DBTYPE_DBTIMESTAMP`||授予配额的时间。|  
|`LastRequestTime`|**DBTYPE_DBTIMESTAMP**||上次修改配额请求的时间。|  
|`MemoryUsed`|`DBTYPE_I4`||在与配额建立关联时使用的内存量。|  
|`MemoryGranted`|`DBTYPE_I4`||授予给获取内存配额的作业以供其使用的内存量。|  
|`Blocked`|`DBTYPE_BOOL`||一个布尔值，该值指示作业的阻止状态。 如果为 True，则表示将阻止作业以等待其他作业释放足够的配额来授予其配额请求。 如果为 False，则表示作业已收到其配额且可执行。|  
  
 未对此架构行集进行排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|ReplTest1|  
|--------------|-----------|  
|GUID|a07ccd23-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|MemoryGrant|  
  
## <a name="see-also"></a>请参阅  
 [XML for Analysis 架构行集](xml-for-analysis-schema-rowsets.md)  
  
  
