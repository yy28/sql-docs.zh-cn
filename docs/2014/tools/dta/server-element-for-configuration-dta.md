---
title: 配置 (DTA) 的服务器元素 |Microsoft 文档
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
- Server element
ms.assetid: da9ff870-9cfd-42fe-994b-7b9292681f7d
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 131885c5e9547767dece2240bcbd64c06b5e4a61
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014239"
---
# <a name="server-element-for-configuration-dta"></a>配置的服务器元素 (DTA)
  包含的数据库引擎优化顾问来评估其假设配置的服务器的标识信息 (通过指定`Configuration`元素)。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Configuration>  
    <Server>  
...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|一次每个`Configuration`元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[配置元素&#40;DTA&#41;](configuration-element-dta.md)|  
|**子元素**|[服务器的名称元素&#40;DTA&#41;](name-element-for-server-dta.md)<br /><br /> [有关配置的数据库元素&#40;DTA&#41;](database-element-for-configuration-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 你可以指定只有一个`Server`元素`Configuration`元素。 在 **数据库引擎优化顾问 XML 架构** 中，此元素的名称为 [ServerTypecomplexType](http://go.microsoft.com/fwlink/?linkid=43100)。 请勿将此`Server`替换的子元素`DTAInput`元素。 有关详细信息，请参阅[服务器元素 (DTA)](server-element-dta.md)。  
  
## <a name="example"></a>示例  
 有关用法示例，请参阅[具有用户指定配置 (DTA) 的 XML 输入文件示例](xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  