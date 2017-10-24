---
title: "DiagnosticInformation 元素 (ssbdiagnose) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML output file format [ssbdiagnose], diagnosticinformation element
- diagnosticinformation element
- ssbdiagnose
ms.assetid: 0cfda544-542c-4cf4-86d2-8031c91b10f6
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9d5a21ac18d6b4982c7c93bf11e3bf16051dc0c7
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="diagnosticinformation-element-ssbdiagnose"></a>DiagnosticInformation 元素 (ssbdiagnose)
  **DiagnosticInformation** 元素包含报告实用工具发现的诊断信息的所有元素。 **DiagnosticInformation** 是 **ssbdiagnostic** XML 输出文件的根元素。  
  
## <a name="syntax"></a>语法  
  
```  
  
<DiagnosticInformation>   
    ...   
</DiagnosticInformation>  
```  
  
## <a name="element-attributes"></a>元素属性  
  
|Attribute|说明|  
|---------------|-----------------|  
|**无**|N/A|  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|每个 **ssbdiagnose** XML 输出文件一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|无。|  
|**子元素**|[Banner 元素 &#40; ssbdiagnose &#41;](../../tools/ssbdiagnose/banner-element-ssbdiagnose.md)<br /><br /> [Issue 元素 &#40; ssbdiagnose &#41;](../../tools/ssbdiagnose/issue-element-ssbdiagnose.md)|  
  
## <a name="remarks"></a>注释  
 有关 XML namespaces 的详细信息，请参阅 [MSDN Library 中的](http://go.microsoft.com/fwlink/?LinkId=7341) Namespaces in an XML Document [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
## <a name="see-also"></a>另请参阅  
 [ssbdiagnose 实用工具 &#40;Service Broker &#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  

