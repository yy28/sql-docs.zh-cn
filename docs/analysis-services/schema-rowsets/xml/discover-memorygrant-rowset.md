---
title: DISCOVER_MEMORYGRANT 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a19d5520e15df761dc019a994edf7b794ac1eb0f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34027627"
---
# <a name="discovermemorygrant-rowset"></a>DISCOVER_MEMORYGRANT 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  返回由当前正在服务器上运行的作业占用的内部内存配额授予的列表。 若要查明作业是否在服务器上运行，请使用 `Select * from $System.Discover_Jobs`。  
  
 **适用于：** 表格模型、 多维模型  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_MEMORYGRANT**行集包含以下各列。  
  
|列名|类型指示符|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**MEMORY_ID**|**DBTYPE_I8**||用于标识内存配额授予的数字。 在单个 DISCOVER_MEMORYGRANT 请求的上下文中是唯一的。|  
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
  
  
