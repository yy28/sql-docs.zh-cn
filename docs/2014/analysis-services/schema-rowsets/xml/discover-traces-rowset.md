---
title: DISCOVER_TRACES 行集 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 1be6a035-ffc9-489e-9d4d-7391b3e384e2
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7b3c8428b34a72f16986044db1652b9907384b07
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124874"
---
# <a name="discovertraces-rowset"></a>DISCOVER_TRACES 行集
  提供有关服务器上当前活动的跟踪的信息。  
  
 **适用于：** 表格模型、 多维模型  
  
## <a name="rowset-columns"></a>行集列  
 `DISCOVER_TRACES`行集包含以下各列。  
  
|列名|类型指示符|Description|  
|-----------------|--------------------|-----------------|  
|`TraceID`|`DBTYPE_WSTR`|跟踪 id。|  
|`TraceName`|`DBTYPE_WSTR`|跟踪名称。|  
|`LogFileName`|`DBTYPE_WSTR`|跟踪日志文件名。|  
|`LogFileSize`|`DBTYPE_I4`|跟踪日志文件大小。|  
|`LogFileRollover`|`DBTYPE_BOOL`|如果为 true，则表示应翻转日志文件；否则为 false。|  
|`AutoRestart`|`DBTYPE_BOOL`|如果为 true，则表示启用了自动重新启动选项；否则为 false。|  
|`CreationTime`|`DBTYPE_TIME`|该跟踪的创建日期和时间。|  
|`StopTime`|`DBTYPE_TIME`|跟踪的停止时间。|  
|`Type`|`PF_DBTYPE_WSTR`|跟踪的类型。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 `DISCOVER_TRACES`行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**TraceId**|`DBTYPE_I4`|可选。|  
|`Type`|WSTR|可选。|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|ReplTest1|  
|--------------|-----------|  
|GUID|a07ccd1a-8148-11d0-87bb-00c04fc33942|  
|String|DISCOVER_TRACES|  
  
## <a name="see-also"></a>请参阅  
 [XML for Analysis 架构行集](xml-for-analysis-schema-rowsets.md)  
  
  