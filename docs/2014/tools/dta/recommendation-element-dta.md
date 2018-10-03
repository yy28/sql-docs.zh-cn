---
title: 建议元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Recommendation element
ms.assetid: 679ea535-865a-4633-a4d3-5b3090515158
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 60bc8c4cbd2166a302a0f61176fa198787575f88
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48107050"
---
# <a name="recommendation-element-dta"></a>建议元素 (DTA)
  包含有关属于用户指定配置的假设索引的信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Configuration>  
    ...code removed here...  
    <Table>  
      <Name>...</Name>  
      <Recommendation>  
      ...code removed here...  
      </Recommendation>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|可选。 可以使用上一次为每个`Table`元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[表的架构元素&#40;DTA&#41;](table-element-for-schema-dta.md)|  
|**子元素**|[创建元素&#40;DTA&#41;](create-element-dta.md)<br /><br /> `Drop` 元素。 有关详细信息，请参阅 [数据库引擎优化顾问 XML 架构](http://go.microsoft.com/fwlink/?linkid=43100)。|  
  
## <a name="remarks"></a>备注  
 在数据库引擎优化顾问 XML 架构中，此元素的名称为 **RecommendationTypecomplexType** 。 该元素用于指定假设配置的索引。 请勿将此`Recommendation`具有可用于指定分区的其他类型的元素 (`RecommendationPType`) 或视图 (`RecommendationViewType`)。 有关其他信息`Recommendation`元素类型，请参阅[数据库引擎优化顾问 XML 架构](http://go.microsoft.com/fwlink/?linkid=43100)。  
  
## <a name="example"></a>示例  
 有关此元素的用法示例，请参阅[用户指定配置 (DTA) 的 XML 输入文件示例](xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
