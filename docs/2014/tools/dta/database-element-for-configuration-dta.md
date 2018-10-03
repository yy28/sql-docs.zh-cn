---
title: 配置 (DTA) 数据库元素 |Microsoft Docs
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
ms.assetid: e91ba243-6cc9-457a-8f5a-134f3c71ae69
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1a3547d10f325e047174f7106267b480084e88df
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48062021"
---
# <a name="database-element-for-configuration-dta"></a>用于配置的数据库元素 (DTA)
  指定要对其数据库引擎优化顾问评估其假设配置的数据库 (由指定`Configuration`元素)。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|需要一个或多个每次`Server`元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[用于配置的服务器元素&#40;DTA&#41;](server-element-for-configuration-dta.md)|  
|**子元素**|[数据库的名称元素&#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [数据库的架构元素&#40;DTA&#41;](schema-element-for-database-dta.md)<br /><br /> [建议元素&#40;DTA&#41;](recommendation-element-dta.md)|  
  
## <a name="remarks"></a>备注  
 在数据库引擎优化顾问 XML 架构中，此元素的名称为 **DatabaseTypecomplexType** 。 不要将此 `Database` 元素与其根父为 `Server` 元素的元素（出现在 XML 输入文件的顶部）混淆。 有关详细信息，请参阅[服务器的数据库元素 (DTA)](database-element-for-server-dta.md)。  
  
## <a name="example"></a>示例  
 有关用法示例的这`Database`元素，请参阅[XML 输入文件示例使用用户指定配置&#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
