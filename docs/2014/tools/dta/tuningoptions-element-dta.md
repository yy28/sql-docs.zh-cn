---
title: TuningOptions 元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- TuningOptions element
ms.assetid: 58a22ba1-8e03-411f-bd46-85e4540f217a
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30447544b7c2fbfa9bfbe5e8a992605af65da5ca
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37261823"
---
# <a name="tuningoptions-element-dta"></a>TuningOptions 元素 (DTA)
  包含用于特定优化会话的优化选项。  
  
## <a name="syntax"></a>语法  
  
```  
  
<DTAInput>  
    <Server>  
...code removed...  
    <Workload>...</Workload>  
    <TuningOptions>...</TuningOptions>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|可选。 如果使用，可以仅使用一次为每个`DTAInput`元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[DTAInput 元素&#40;DTA&#41;](dtainput-element-dta.md)|  
|**子元素**|`ReportSet` 元素。 有关详细信息，请参阅 [数据库引擎优化顾问 XML 架构](http://go.microsoft.com/fwlink/?linkid=43100)。<br /><br /> `TuningLogTable` 元素。 有关详细信息，请参阅 [数据库引擎优化顾问 XML 架构](http://go.microsoft.com/fwlink/?linkid=43100)。<br /><br /> `NumberOfEvents` 元素。 有关详细信息，请参阅 [数据库引擎优化顾问 XML 架构](http://go.microsoft.com/fwlink/?linkid=43100)。<br /><br /> [TuningTimeInMin 元素&#40;DTA&#41;](tuningtimeinmin-element-dta.md)<br /><br /> [StorageBoundInMB 元素&#40;DTA&#41;](storageboundinmb-element-dta.md)<br /><br /> `MaxKeyColumnsInIndex` 元素。 有关详细信息，请参阅 [数据库引擎优化顾问 XML 架构](http://go.microsoft.com/fwlink/?linkid=43100)。<br /><br /> `MaxColumnsInIndex` 元素。 有关详细信息，请参阅 [数据库引擎优化顾问 XML 架构](http://go.microsoft.com/fwlink/?linkid=43100)。<br /><br /> `MinPercentageImprovement` 元素。 有关详细信息，请参阅 [数据库引擎优化顾问 XML 架构](http://go.microsoft.com/fwlink/?linkid=43100)<br /><br /> [TestServer 元素&#40;DTA&#41;](server-element-dta.md)<br /><br /> [FeatureSet 元素&#40;DTA&#41;](featureset-element-dta.md)<br /><br /> [分区元素&#40;DTA&#41;](partitioning-element-dta.md)<br /><br /> [DropOnlyMode 元素&#40;DTA&#41;](droponlymode-element-dta.md)<br /><br /> [KeepExisting 元素&#40;DTA&#41;](keepexisting-element-dta.md)<br /><br /> [OnlineIndexOperation 元素&#40;DTA&#41;](onlineindexoperation-element-dta.md)<br /><br /> [DatabaseToConnect 元素&#40;DTA&#41;](databasetoconnect-element-dta.md)<br /><br /> `IgnoreConstantsInWorkload` 元素。 有关详细信息，请参阅 [数据库引擎优化顾问 XML 架构](http://go.microsoft.com/fwlink/?linkid=43100)。<br /><br /> `RetainShellDB` 元素。 有关详细信息，请参阅 [数据库引擎优化顾问 XML 架构](http://go.microsoft.com/fwlink/?linkid=43100)。|  
  
## <a name="example"></a>示例  
 有关的示例`TuningOptions`元素，请参阅[XML 输入文件示例&#40;DTA&#41;](xml-input-file-samples-dta.md)。  
  
## <a name="see-also"></a>请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
