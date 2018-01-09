---
title: "DISCOVER_MEMORYUSAGE 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: e416ea61-9615-468c-a96f-bbf731f803b1
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bd97d1b2eb02dda3f8add861e6767b7a495a821d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="discovermemoryusage-rowset"></a>DISCOVER_MEMORYUSAGE 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]返回分配的服务器的各种对象的 DISCOVER_MEMORYUSAGE 统计信息。  
  
> [!WARNING]  
>  此行集可生成大型结果集。 如果因结果所需的显示内存超过 SQL Server Management Studio 所允许的显示内存而导致结果无法显示，则结果将写入位于以下默认位置的临时文件：  
>   
>  \<驱动器 >: \Users\\< 用户名\>\AppData\Local\Temp\\< fileID\>.xml'。  
  
 **适用于：**表格模型、 多维模型  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_MEMORYUSAGE**行集包含以下各列。  
  
|列名|类型指示符|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**MemoryID**|**DBTYPE_UI8**||标识内存的数字。|  
|**MemoryName**|**DBTYPE_WSTR**||拥有内存的对象的名称。|  
|**SPID**|**DBTYPE_UI4**|是|分配内存的会话。 零指示内存未与特定会话关联。|  
|**CreationTime**|**DBTYPE_DBTIMESTAMP**||输入“创建对象的时间”或“分配内存的时间”。|  
|**BaseObjectType**|**DBTYPE_UI4**|是|这是描述对象类型的数字。 带相同的 BaseObjectType 的对象具有同一类型。|  
|**MemoryUsed**|**DBTYPE_UI8**|是|这是对象的当前大小，它可能小于分配给对象以供其使用的内存。|  
|**MemoryAllocated**|**DBTYPE_UI8**||分配给对象以供其使用的内存量，它可能大于对象实际使用的内存量。|  
|**MemoryAllocBase**|**DBTYPE_UI8**||最初分配给对象的字节数（不包括针对对象内容的额外分配）。|  
|**MemoryAllocFromAlloc**|**DBTYPE_UI8**||为此对象的内容分配的内存。|  
|**ElementCount**|**DBTYPE_UI4**||对于容器对象，这是该对象包含的对象的数目。|  
|**收缩**|**DBTYPE_BOOL**|是|一个布尔值，指示内存是否可收缩（可能因内存压力被逐出）。 如果为 true，则表示内存可收缩；如果为 false，则表示内存不可收缩。|  
|**ObjectParentPath**|**DBTYPE_WSTR**||用于标识此对象的完整路径的字符串。|  
|**Exchange Spill**|**DBTYPE_WSTR**||标识对象的字符串。 由字符串表示此对象的完整路径: (ObjectParentPath + '。 ' + ObjectId)。|  
  
 未对此架构行集进行排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|ReplTest1|  
|--------------|-----------|  
|GUID|A07CCD21-8148-11D0-87BB-00C04FC33942|  
|ADOMDNAME|MemoryUsage|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
