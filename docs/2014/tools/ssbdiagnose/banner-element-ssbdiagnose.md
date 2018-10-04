---
title: Banner 元素 (ssbdiagnose) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- banner element
- XML output file format [ssbdiagnose], banner element
- ssbdiagnose
ms.assetid: cc6cd49a-acf0-4cfb-8c6a-554692b89de2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b461370b4bbab4cc7e28bcb1ed95d0a3e6d5553e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48080737"
---
# <a name="banner-element-ssbdiagnose"></a>Banner 元素 (ssbdiagnose)
  标识生成 **ssbdiagnose** 输出 XML 文件的实用工具。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Banner  
    title="..."   
    product="..."   
    version="..." />  
```  
  
## <a name="element-attributes"></a>元素属性  
  
|Attribute|Description|  
|---------------|-----------------|  
|`title`|标识生成 **ssbdiagnose** XML 输出文件的实用工具。|  
|`product`|标识生成 **ssbdiagnose** XML 输出文件的产品。|  
|`version`|标识生成 XML 输出文件的实用工具的版本。|  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|每个 **ssbdiagnose** 输出 XML 文件出现一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[DiagnosticInformation 元素&#40;ssbdiagnose&#41;](diagnosticinformation-element-ssbdiagnose.md)|  
|**子元素**|无。|  
  
## <a name="example"></a>示例  
 这是一个 Banner 元素的示例。  
  
```  
<Banner title="Service Broker Diagnostics Utility" product="Microsoft SQL Server" version="10.0.1073.0" />  
```  
  
## <a name="see-also"></a>请参阅  
 [ssbdiagnose 实用工具 (Service Broker)](ssbdiagnose-utility-service-broker.md)  
  
  
