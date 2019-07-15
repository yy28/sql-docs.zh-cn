---
title: Banner 元素 (ssbdiagnose) |Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- banner element
- XML output file format [ssbdiagnose], banner element
- ssbdiagnose
ms.assetid: cc6cd49a-acf0-4cfb-8c6a-554692b89de2
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2846f35b8cd8f99d61a70fe355ac5077fcb00eb9
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67732039"
---
# <a name="banner-element-ssbdiagnose"></a>Banner 元素 (ssbdiagnose)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  标识生成 **ssbdiagnose** 输出 XML 文件的实用工具。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Banner  
    title="..."   
    product="..."   
    version="..." />  
```  
  
## <a name="element-attributes"></a>元素属性  
  
|Attribute|描述|  
|---------------|-----------------|  
|**title**|标识生成 **ssbdiagnose** XML 输出文件的实用工具。|  
|**product**|标识生成 **ssbdiagnose** XML 输出文件的产品。|  
|**version**|标识生成 XML 输出文件的实用工具的版本。|  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|描述|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|每个 **ssbdiagnose** 输出 XML 文件出现一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[DiagnosticInformation 元素 (ssbdiagnose)](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)|  
|**子元素**|无。|  
  
## <a name="example"></a>示例  
 这是一个 Banner 元素的示例。  
  
```  
<Banner title="Service Broker Diagnostics Utility" product="Microsoft SQL Server" version="10.0.1073.0" />  
```  
  
## <a name="see-also"></a>另请参阅  
 [ssbdiagnose 实用工具 (Service Broker)](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
