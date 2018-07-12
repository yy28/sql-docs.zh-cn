---
title: DatabaseToConnect 元素 (DTA) |Microsoft Docs
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
- DatabaseToConnect element
ms.assetid: 65153a66-3aee-4429-99b7-0816ac23c285
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9a29e28782207d5da0e3166669c6c38a7119f597
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37161588"
---
# <a name="databasetoconnect-element-dta"></a>DatabaseToConnect 元素 (DTA)
  指定数据库引擎优化顾问在优化工作负荷时连接到的第一个数据库。  
  
## <a name="syntax"></a>语法  
  
```  
  
    <TuningOptions>  
...code removed here...  
      <DatabaseToConnect>...</DatabaseToConnect>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|**数据类型和长度**|`string`长度没有限制。|  
|**默认值**|无。|  
|**出现次数**|可选。 可以使用上一次为每个`TuningOptions`元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素&#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**子元素**|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 使用`DatabaseToConnect`以指定希望数据库引擎优化顾问在启动优化会话时连接到的第一个数据库的名称。 此元素只能指定一个数据库。 如果指定了多个数据库名称，数据库引擎优化顾问将返回错误。  
  
## <a name="example"></a>示例  
 有关使用示例，请参阅[使用内联工作负荷的 XML 输入文件示例 (DTA)](xml-input-file-sample-with-inline-workload-dta.md)。  
  
## <a name="see-also"></a>请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
