---
title: EventString 元素 (DTA) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- EventString element
ms.assetid: f76c37b4-2f6e-4274-8ee2-87e89d98e8a2
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6155627f60694cf1a21d39893e40b106b9df0886
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016507"
---
# <a name="eventstring-element-dta"></a>EventString 元素 (DTA)
  直接在 XML 输入文件中指定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本工作负荷。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Workload>  
    <EventString Weight="...">  
    ...code removed here...  
    </EventString>  
</Workload>  
```  
  
## <a name="element-attributes"></a>元素属性  
  
|Attribute|Description|  
|---------------|-----------------|  
|`Weight`|可选。 为指定的事件指定查询加权系数（重要性系数）。 使用`float`数据类型指定加权。 例如，`Weight`="100.01"。 可为 `Weight` 指定的最小值为“0”。|  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|**数据类型和长度**|`string`长度不受限制。|  
|**默认值**|无。|  
|**出现次数**|如果未指定其他类型的工作负荷，则必须使用一次。 必须指定`EventString`、 `File`，或`Database`子元素`Workload`父，但仅有一个类型使用。 例如，如果指定具有的工作负荷`EventString`元素，则你不能同时指定具有的工作负荷`File`相同的 XML 输入文件中的元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[工作负荷元素&#40;DTA&#41;](workload-element-dta.md)|  
|**子元素**|无。|  
  
## <a name="example"></a>示例  
 有关该元素的使用示例，请参阅[使用内联工作负荷的 XML 输入文件示例 (DTA)](xml-input-file-sample-with-inline-workload-dta.md)。  
  
## <a name="see-also"></a>请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  