---
title: 服务器 (DTA) 数据库元素 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 341c267b686a56a37390e0ee774df0aa20e73fd8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049817"
---
# <a name="database-element-for-server-dta"></a>服务器的数据库元素 (DTA)
  指定特定服务器上要优化的数据库。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|无。|  
|默认值|无。|  
|出现次数|需要一个或多个每次`Server`元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|父元素|[服务器元素&#40;DTA&#41;](server-element-dta.md)|  
|子元素|[数据库的名称元素&#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [数据库的架构元素&#40;DTA&#41;](schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>备注  
 在数据库引擎优化顾问 XML 架构中，此元素的名称为 **DatabaseDetailsTypecomplexType** 。 请不要将此 `Database` 元素与根级父元素为 `Configuration` 元素的元素相混淆。 有关详细信息，请参阅[用于配置的数据库元素 (DTA)](database-element-for-configuration-dta.md)。  
  
## <a name="example"></a>示例  
 有关用法示例`Database`元素，请参阅[服务器元素&#40;DTA&#41;](server-element-dta.md)。  
  
## <a name="see-also"></a>请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
