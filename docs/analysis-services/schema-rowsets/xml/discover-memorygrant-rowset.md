---
title: "DISCOVER_MEMORYGRANT 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: d254e42d-9918-47ce-b6df-47f1f0b432dd
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 38eb6dae47c01758b3ca3b5c04794014b247b495
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="discovermemorygrant-rowset"></a>DISCOVER_MEMORYGRANT 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]返回列表的内部内存配额授予执行的服务器当前运行的作业。 若要查明作业是否在服务器上运行，请使用 `Select * from $System.Discover_Jobs`。  
  
 **适用于：**表格模型、 多维模型  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_MEMORYGRANT**行集包含以下各列。  
  
|列名|类型指示符|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**MEMORY_ID**|**是 DBTYPE_I8**||用于标识内存配额授予的数字。 在单个 DISCOVER_MEMORYGRANT 请求的上下文中是唯一的。|  
|**SPID**|**DBTYPE_I4**|必需|SPID，可通过运行 `Select * from $System.Discover_Sessions` 获得它。|  
|**CreationTime**|**是 DBTYPE_I8 DBTYPE_DBTIMESTAMP**||授予配额的时间。|  
|**LastRequestTime**|**DBTYPE_DBTIMESTAMP**||上次修改配额请求的时间。|  
|**MemoryUsed**|**DBTYPE_I4**||在与配额建立关联时使用的内存量。|  
|**MemoryGranted**|**DBTYPE_I4**||授予给获取内存配额的作业以供其使用的内存量。|  
|**阻止**|**DBTYPE_BOOL**||一个布尔值，该值指示作业的阻止状态。 如果为 True，则表示将阻止作业以等待其他作业释放足够的配额来授予其配额请求。 如果为 False，则表示作业已收到其配额且可执行。|  
  
 未对此架构行集进行排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|值|  
|--------------|-----------|  
|GUID|a07ccd23-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|MemoryGrant|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
