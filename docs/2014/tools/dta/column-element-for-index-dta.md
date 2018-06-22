---
title: 列索引的元素 (DTA) |Microsoft 文档
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
- Column element
ms.assetid: ba9fac20-26bd-4333-940e-842c15241b46
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 58d8827fe160ef1acb300e7501fd9faeaa369efd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015145"
---
# <a name="column-element-for-index-dta"></a>索引的列元素 (DTA)
  指定在其上为用户指定的配置创建索引的列。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Create>  
  <Index>  
    <Name>...</Name>  
    <Column [Type | SortOrder]>  
     ...code removed here...  
     </Column>  
```  
  
## <a name="element-attributes"></a>元素属性  
  
|列属性|Description|  
|----------------------|-----------------|  
|`Type`|可选。 指定索引列类型。 使用 string 数据类型将此属性指定为以下允许  值之一：<br /><br /> `KeyColumn`：<br />                  指定按索引键进行引用的列。 使用下面的语法设置此属性：<br />`<Column Type="KeyColumn">`<br />有关键列的详细信息，请参阅 [群集索引和非群集索引介绍](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)。<br /><br /> `IncludedColumn`： 指定列是包含性列 （而不是键列）。 使用下面的语法设置此属性：<br />`<Column Type="IncludedColumn">`<br />有关包含列的详细信息，请参阅 [创建带有包含列的索引](../../relational-databases/indexes/create-indexes-with-included-columns.md)。|  
|`SortOrder`|可选。 指定列的排序顺序。 请使用 **string** 数据类型按如下格式指定 **Ascending** 或 **Descending** 排序顺序：<br /><br /> `<Column SortOrder="Ascending">`|  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|最多可以为 `Index` 元素指定 1024 列。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[索引元素&#40;DTA&#41;](index-element-dta.md)|  
|**子元素**|[列的名称元素&#40;DTA&#41;](name-element-for-column-dta.md)|  
  
## <a name="example"></a>示例  
 有关此元素的用法示例，请参阅[用户指定配置 (DTA) 的 XML 输入文件示例](xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  