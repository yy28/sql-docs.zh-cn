---
title: 架构的表元素（DTA） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Table element [DTA]
ms.assetid: a59e8319-05d1-47f3-af39-7d970ab8e7dc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8b3a72f800643afa5e7edf6bdfa9928196f5da2d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63138779"
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
|`NumberOfRows`|可选。 允许您模拟不同大小的表的整数。|  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|描述|  
|--------------------|-----------------|  
|**数据类型和长度**|**string**，介于1到255个字符之间。|  
|**默认值**|无。|  
|**匹配项**|可选。 列出数量与工作负荷相当的表。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[数据库的架构元素 (DTA)](schema-element-for-database-dta.md)|  
|**子元素**|[表的名称元素 (DTA)](name-element-for-table-dta.md)|  
  
## <a name="remarks"></a>备注  
 如果不指定 `Table` 元素，则数据库引擎优化顾问将假定指定数据库中的所有表都可优化。  
  
## <a name="example"></a>示例  
 有关使用示例，请参阅[服务器元素 (DTA)](server-element-dta.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
