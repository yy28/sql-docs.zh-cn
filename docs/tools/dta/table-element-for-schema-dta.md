---
title: 架构的表元素 (DTA)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Table element [DTA]
ms.assetid: a59e8319-05d1-47f3-af39-7d970ab8e7dc
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 419420c9d1ecec501ca8a7d92ef6a23a658db713
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75307864"
---
# <a name="table-element-for-schema-dta"></a>架构的表元素 (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

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
|**父元素**|[数据库的架构元素 (DTA)](../../tools/dta/schema-element-for-database-dta.md)|  
|**子元素**|[表的名称元素 (DTA)](../../tools/dta/name-element-for-table-dta.md)|  
  
## <a name="remarks"></a>备注  
 如果不指定 **Table** 元素，则数据库引擎优化顾问将假定指定数据库中的所有表都可优化。  
  
## <a name="example"></a>示例  
 有关使用示例，请参阅[服务器元素 (DTA)](../../tools/dta/server-element-dta.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
