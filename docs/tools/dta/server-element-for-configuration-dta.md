---
title: "配置 (DTA) 的服务器元素 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: Server element
ms.assetid: da9ff870-9cfd-42fe-994b-7b9292681f7d
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 98d5e308830cf8ba07553b4abb3c1ffa1de37d84
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="server-element-for-configuration-dta"></a>配置的服务器元素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]包含的数据库引擎优化顾问来评估其假设配置的服务器的标识信息 (通过指定**配置**元素)。  
  
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
|**出现次数**|每个 **Configuration** 元素必须出现一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[配置元素 (DTA)](../../tools/dta/configuration-element-dta.md)|  
|**子元素**|[服务器的名称元素 (DTA)](../../tools/dta/name-element-for-server-dta.md)<br /><br /> [配置的数据库元素 (DTA)](../../tools/dta/database-element-for-configuration-dta.md)|  
  
## <a name="remarks"></a>注释  
 只能为 **Server** 元素指定一个 **Configuration** 元素。 在 **数据库引擎优化顾问 XML 架构** 中，此元素的名称为 [ServerTypecomplexType](http://go.microsoft.com/fwlink/?linkid=43100)。 请不要将此 **Server** 元素与 **DTAInput** 元素的子元素混淆。 有关详细信息，请参阅[服务器元素 (DTA)](../../tools/dta/server-element-dta.md)。  
  
## <a name="example"></a>示例  
 有关用法示例，请参阅[具有用户指定配置 (DTA) 的 XML 输入文件示例](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
