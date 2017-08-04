---
title: "DatabaseToConnect 元素 (DTA) |Microsoft 文档"
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
- DatabaseToConnect element
ms.assetid: 65153a66-3aee-4429-99b7-0816ac23c285
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 94746d3007587223ba1b2ae6a3868ce3a013bafd
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# DatabaseToConnect 元素 (DTA)
  指定数据库引擎优化顾问在优化工作负荷时连接到的第一个数据库。  
  
## 语法  
  
```  
  
    <TuningOptions>  
...code removed here...  
      <DatabaseToConnect>...</DatabaseToConnect>  
```  
  
## 元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|**string**，长度没有限制。|  
|**默认值**|无。|  
|**出现次数**|可选。 对于每个 **TuningOptions** 元素可以使用一次。|  
  
## 元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素 &#40; DTA &#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**子元素**|无|  
  
## 注释  
 使用 **DatabaseToConnect** ，可以指定希望数据库引擎优化顾问在启动优化会话时连接到的第一个数据库的名称。 此元素只能指定一个数据库。 如果指定了多个数据库名称，数据库引擎优化顾问将返回错误。  
  
## 示例  
 有关使用示例，请参阅[使用内联工作负荷的 XML 输入文件示例 (DTA)](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md)。  
  
## 另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
