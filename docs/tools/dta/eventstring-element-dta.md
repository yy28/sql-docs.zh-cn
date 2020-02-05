---
title: EventString 元素 (DTA)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- EventString element
ms.assetid: f76c37b4-2f6e-4274-8ee2-87e89d98e8a2
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: a0bf4fe2b768fd0a9f714540946a84c126aa1679
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75307697"
---
# <a name="eventstring-element-dta"></a>EventString 元素 (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

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
  
|Attribute|说明|  
|---------------|-----------------|  
|**Weight**|可选。 为指定的事件指定查询加权系数（重要性系数）。 使用 **float** 数据类型指定加权。 例如， **Weight**="100.01"。 可为 **Weight** 指定的最小值为“0”。|  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|**string**，无限长。|  
|**默认值**|无。|  
|**出现次数**|如果未指定其他类型的工作负荷，则必须使用一次。 必须为父元素 **EventString**指定子元素 **File**、 **Database** 或 **Workload** ，但只能使用一种类型。 例如，如果指定了具有 **EventString** 元素的工作负荷，则不能在相同的 XML 输入文件中指定具有 **File** 元素的工作负荷。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[工作负荷元素 (DTA)](../../tools/dta/workload-element-dta.md)|  
|**子元素**|无。|  
  
## <a name="example"></a>示例  
 有关该元素的使用示例，请参阅[使用内联工作负荷的 XML 输入文件示例 (DTA)](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
