---
title: DISCOVER_TRANSACTIONS 行集 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 85789177-c5df-4336-a90c-c20d69277ab4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9b0f8c8dc1a289eaa96325ba22aa2e7dc864fb84
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103948"
---
# <a name="discovertransactions-rowset"></a>DISCOVER_TRANSACTIONS 行集
  返回系统上当前挂起的一组事务。  
  
 **适用于：** 表格模型和多维模型  
  
## <a name="rowset-columns"></a>行集列  
 `DISCOVER_TRANSACTIONS`行集包含以下列。  
  
|列名|类型指示符|Description|  
|-----------------|--------------------|-----------------|  
|`TRANSACTION_ID`|`DBTYPE_WSTR`|事务唯一标识符，以 GUID 形式表示。|  
|`TRANSACTION_SESSION_ID`|`DBTYPE_WSTR`|事务会话的唯一标识符，以 GUID 形式表示。|  
|`TRANSACTION_START_TIME`|`DBTYPE_DBTIMESTAMP`|事务开始时的服务器 UTC 日期和时间。|  
|`TRANSACTION_ELAPSED_TIME_MS`|`DBTYPE_I8`|自事务开始起经过的时间（毫秒）。|  
|`TRANSACTION_CPU_TIME_MS`|`DBTYPE_I8`|自事务开始后所有请求占用的 CPU 时间（毫秒）。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 `DISCOVER_TRANSACTIONS`行集可以限制下表中列出的列。  
  
|**列名**|**类型指示符**|**限制状态**|  
|---------------------|------------------------|---------------------------|  
|`ID`|`DBTYPE_WSTR`|可选。|  
|`SESSION_ID`|`DBTYPE_WSTR`|可选。|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|ReplTest1|  
|--------------|-----------|  
|GUID|a07ccd28-8148-11d0-87bb-00c04fc33942|  
|String|DISCOVER_TRANSACTIONS|  
  
## <a name="see-also"></a>请参阅  
 [XML for Analysis 架构行集](xml-for-analysis-schema-rowsets.md)  
  
  
