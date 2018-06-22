---
title: 配置 (DTA) 的数据库元素 |Microsoft 文档
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
- Database element
ms.assetid: e91ba243-6cc9-457a-8f5a-134f3c71ae69
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6afd8b418cd00c2ec89430e4c82613ea1af285d6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016714"
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
|**出现次数**|需要一个或多个一次`Server`元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[配置的服务器元素&#40;DTA&#41;](server-element-for-configuration-dta.md)|  
|**子元素**|[数据库的名称元素&#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [数据库的架构元素&#40;DTA&#41;](schema-element-for-database-dta.md)<br /><br /> [建议元素&#40;DTA&#41;](recommendation-element-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 在数据库引擎优化顾问 XML 架构中，此元素的名称为 **DatabaseTypecomplexType** 。 不要将此 `Database` 元素与其根父为 `Server` 元素的元素（出现在 XML 输入文件的顶部）混淆。 有关详细信息，请参阅[服务器的数据库元素 (DTA)](database-element-for-server-dta.md)。  
  
## <a name="example"></a>示例  
 有关此用法示例`Database`元素，请参阅[使用用户指定配置的 XML 输入文件示例&#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  