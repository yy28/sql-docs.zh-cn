---
title: 创建元素 (DTA) |Microsoft 文档
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
- Create element (DTA)
ms.assetid: 9d076c90-f933-45f4-b6d9-447793f6528b
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ce464bc186e4e99d14cf17d0bc442abee0fed39a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125049"
---
# <a name="create-element-dta"></a>创建元素 (DTA)
  包含有关用户指定配置中的索引、统计信息或堆结构的信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Recommendation>  
    <Create>  
    ...code removed here...  
    </Create>  
</Recommendation>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|对每个物理设计结构类型（索引、统计或堆结构）只需使用一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[建议元素&#40;DTA&#41;](recommendation-element-dta.md)|  
|**子元素**|[索引元素&#40;DTA&#41;](index-element-dta.md)<br /><br /> `Statistics` 元素 (请参阅[数据库引擎优化顾问 XML 架构](http://schemas.microsoft.com/sqlserver/)信息)<br /><br /> `Heap` 元素 (请参阅[数据库引擎优化顾问 XML 架构](http://schemas.microsoft.com/sqlserver/)信息)|  
  
## <a name="remarks"></a>Remarks  
 在数据库引擎优化顾问 XML 架构中，此元素的名称为 **CreateTypecomplexType** 。 此元素用于为用户指定的配置创建索引、统计信息和堆结构。 请勿将此 `Create` 元素和其他可用于创建视图 (`CreateViewType`) 或分区 (`CreatePType`) 的其他类型混淆。 请参阅[数据库引擎优化顾问 XML 架构](http://schemas.microsoft.com/sqlserver/)有关这些其他信息`Create`元素类型。  
  
## <a name="example"></a>示例  
 有关此元素的用法示例，请参阅[用户指定配置 (DTA) 的 XML 输入文件示例](xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  