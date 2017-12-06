---
title: "创建元素 (DTA) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: Create element (DTA)
ms.assetid: 9d076c90-f933-45f4-b6d9-447793f6528b
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ca74ccda2f75dd9af45cc4169a6122dcb8cccdb9
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="create-element-dta"></a>创建元素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]包含有关索引、 统计信息或堆结构中一个用户指定的配置信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Recommendation>  
    <Create>  
    ...code removed here...  
    </Create>  
</Recommendation>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|对每个物理设计结构类型（索引、统计或堆结构）只需使用一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[建议元素 (DTA)](../../tools/dta/recommendation-element-dta.md)|  
|**子元素**|[索引元素 (DTA)](../../tools/dta/index-element-dta.md)<br /><br /> **Statistics** 元素（有关信息，请参阅 [数据库引擎优化顾问 XML 架构](http://schemas.microsoft.com/sqlserver/) ）<br /><br /> **Heap** 元素（有关信息，请参阅 [数据库引擎优化顾问 XML 架构](http://schemas.microsoft.com/sqlserver/) ）|  
  
## <a name="remarks"></a>注释  
 在数据库引擎优化顾问 XML 架构中，此元素的名称为 **CreateTypecomplexType** 。 此元素用于为用户指定的配置创建索引、统计信息和堆结构。 请勿将此 **Create** 元素和其他可用于创建视图 (**CreateViewType**) 或分区 (**CreatePType**) 的其他类型混淆。 有关其他 [Create](http://schemas.microsoft.com/sqlserver/) 元素类型的信息，请参阅 **数据库引擎优化顾问 XML 架构** 。  
  
## <a name="example"></a>示例  
 有关此元素的用法示例，请参阅[用户指定配置 (DTA) 的 XML 输入文件示例](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
