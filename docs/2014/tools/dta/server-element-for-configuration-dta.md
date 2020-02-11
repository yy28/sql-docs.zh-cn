---
title: 用于配置的服务器元素（DTA） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Server element
ms.assetid: da9ff870-9cfd-42fe-994b-7b9292681f7d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2bc763d621d15f982a2670483683d3862e678c98
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63283679"
---
# <a name="server-element-for-configuration-dta"></a>配置的服务器元素 (DTA)
  包含需要数据库引擎优化顾问评估其假设配置（由 `Configuration` 元素指定）的服务器的标识信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Configuration>  
    <Server>  
...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|每个 `Configuration` 元素必须出现一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[配置元素 (DTA)](configuration-element-dta.md)|  
|**子元素**|[服务器的名称元素 (DTA)](name-element-for-server-dta.md)<br /><br /> [配置的数据库元素 (DTA)](database-element-for-configuration-dta.md)|  
  
## <a name="remarks"></a>备注  
 只能为`Configuration`元素指定一个`Server`元素。 在 **数据库引擎优化顾问 XML 架构** 中，此元素的名称为 [ServerTypecomplexType](https://go.microsoft.com/fwlink/?linkid=43100)。 请不要将此 `Server` 元素与 `DTAInput` 元素的子元素混淆。 有关详细信息，请参阅[服务器元素 (DTA)](server-element-dta.md)。  
  
## <a name="example"></a>示例  
 有关用法示例，请参阅[具有用户指定配置 (DTA) 的 XML 输入文件示例](xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
