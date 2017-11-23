---
title: "DatabaseToConnect 元素 (DTA) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: DatabaseToConnect element
ms.assetid: 65153a66-3aee-4429-99b7-0816ac23c285
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 21cf5893c23fda68ed62c1415f54844e60947253
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
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
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|**string**，长度没有限制。|  
|**默认值**|无。|  
|**出现次数**|可选。 对于每个 **TuningOptions** 元素可以使用一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素 (DTA)](../../tools/dta/tuningoptions-element-dta.md)|  
|**子元素**|无|  
  
## <a name="remarks"></a>注释  
 使用 **DatabaseToConnect** ，可以指定希望数据库引擎优化顾问在启动优化会话时连接到的第一个数据库的名称。 此元素只能指定一个数据库。 如果指定了多个数据库名称，数据库引擎优化顾问将返回错误。  
  
## <a name="example"></a>示例  
 有关使用示例，请参阅[使用内联工作负荷的 XML 输入文件示例 (DTA)](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
