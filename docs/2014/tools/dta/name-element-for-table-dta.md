---
title: 表的名称元素（DTA） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Name element
ms.assetid: 422a755f-ee52-4863-b1aa-f4ef1b8fd0bb
author: stevestein
ms.author: sstein
ms.openlocfilehash: cdaf7cc0e4e96f7e58c80a074df636f603d89a6f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85040382"
---
# <a name="name-element-for-table-dta"></a>表的名称元素 (DTA)
  指定表名以进行优化。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Schema>  
    <Table>  
        <Name>...</Name>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|`string`，介于 1 到 255 个字符之间。|  
|**默认值**|无。|  
|**出现次数**|必需。 每个 `Table` 元素一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[架构的表元素 (DTA)](table-element-for-schema-dta.md)|  
|**子元素**|无。|  
  
## <a name="example"></a>示例  
 有关使用示例，请参阅[服务器元素 (DTA)](server-element-dta.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
