---
title: 表 (DTA) 的名称元素 |Microsoft 文档
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
- Name element
ms.assetid: 422a755f-ee52-4863-b1aa-f4ef1b8fd0bb
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 0cb54e42b9acf1ac4b4224feb0c25dcdb98cab8b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138321"
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
  
|特征|Description|  
|--------------------|-----------------|  
|**数据类型和长度**|`string`，介于 1 到 255 个字符之间。|  
|**默认值**|无。|  
|**出现次数**|必需的。 一次为每个`Table`元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[架构的表元素&#40;DTA&#41;](table-element-for-schema-dta.md)|  
|**子元素**|无。|  
  
## <a name="example"></a>示例  
 有关使用示例，请参阅[服务器元素 (DTA)](server-element-dta.md)。  
  
## <a name="see-also"></a>请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  