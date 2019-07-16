---
title: EventString 元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- EventString element
ms.assetid: f76c37b4-2f6e-4274-8ee2-87e89d98e8a2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30e46515fda5bf03a96e9f1168b470f635698d07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211117"
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
  
|特性|描述|  
|---------------|-----------------|  
|`Weight`|可选。 为指定的事件指定查询加权系数（重要性系数）。 使用 `float` 数据类型指定加权。 例如，`Weight`="100.01"。 可为 `Weight` 指定的最小值为“0”。|  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|描述|  
|--------------------|-----------------|  
|**数据类型和长度**|`string`，无限长。|  
|**默认值**|无。|  
|**出现次数**|如果未指定其他类型的工作负荷，则必须使用一次。 必须为父元素 `EventString` 指定子元素 `File`、`Database` 或 `Workload`，但只能使用一种类型。 例如，如果指定了具有 `EventString` 元素的工作负荷，则不能在相同的 XML 输入文件中指定具有 `File` 元素的工作负荷。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[工作负荷元素 (DTA)](workload-element-dta.md)|  
|**子元素**|无。|  
  
## <a name="example"></a>示例  
 有关该元素的使用示例，请参阅[使用内联工作负荷的 XML 输入文件示例 (DTA)](xml-input-file-sample-with-inline-workload-dta.md)。  
  
## <a name="see-also"></a>请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
