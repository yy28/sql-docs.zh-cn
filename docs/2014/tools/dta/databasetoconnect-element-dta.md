---
title: DatabaseToConnect 元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DatabaseToConnect element
ms.assetid: 65153a66-3aee-4429-99b7-0816ac23c285
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4fef2df598d96b33def41f27345f88226fd4c6b5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63185413"
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
|**数据类型和长度**|`string`，长度没有限制。|  
|**默认值**|无。|  
|**出现次数**|可选。 对于每个 `TuningOptions` 元素可以使用一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素 (DTA)](tuningoptions-element-dta.md)|  
|**子元素**|None|  
  
## <a name="remarks"></a>备注  
 使用 `DatabaseToConnect`，可以指定希望数据库引擎优化顾问在启动优化会话时连接到的第一个数据库的名称。 此元素只能指定一个数据库。 如果指定了多个数据库名称，数据库引擎优化顾问将返回错误。  
  
## <a name="example"></a>示例  
 有关使用示例，请参阅[使用内联工作负荷的 XML 输入文件示例 (DTA)](xml-input-file-sample-with-inline-workload-dta.md)。  
  
## <a name="see-also"></a>请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
