---
title: "架构 (DTA) 的表元素 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Table element [DTA]
ms.assetid: a59e8319-05d1-47f3-af39-7d970ab8e7dc
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8786081dfd306de3fdfcf3d407854e49061548a2
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="table-element-for-schema-dta"></a>架构的表元素 (DTA)
  指定用于优化的表。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Schema>  
...code removed here...  
    <Table>...</Table>  
```  
  
## <a name="element-attributes"></a>元素属性  
  
|Attribute|说明|  
|---------------|-----------------|  
|**NumberOfRows**|可选。 允许您模拟不同大小的表的整数。|  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|**字符串**，长度为 1 到 255 个字符。|  
|**默认值**|无。|  
|**出现次数**|可选。 列出数量与工作负荷相当的表。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[数据库 &#40; DTA &#41; 的架构元素](../../tools/dta/schema-element-for-database-dta.md)|  
|**子元素**|[Table &#40; DTA &#41; 的名称元素](../../tools/dta/name-element-for-table-dta.md)|  
  
## <a name="remarks"></a>注释  
 如果不指定 **Table** 元素，则数据库引擎优化顾问将假定指定数据库中的所有表都可优化。  
  
## <a name="example"></a>示例  
 有关使用示例，请参阅[服务器元素 (DTA)](../../tools/dta/server-element-dta.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
