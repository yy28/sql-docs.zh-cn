---
title: DiagnosticInformation 元素 (ssbdiagnose) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- XML output file format [ssbdiagnose], diagnosticinformation element
- diagnosticinformation element
- ssbdiagnose
ms.assetid: 0cfda544-542c-4cf4-86d2-8031c91b10f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8e436911e0d7d6eb1b3d7a6d70befded41e04829
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47665055"
---
# <a name="diagnosticinformation-element-ssbdiagnose"></a>DiagnosticInformation 元素 (ssbdiagnose)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **DiagnosticInformation** 元素包含报告实用工具发现的诊断信息的所有元素。 **DiagnosticInformation** 是 **ssbdiagnostic** XML 输出文件的根元素。  
  
## <a name="syntax"></a>语法  
  
```  
  
<DiagnosticInformation>   
    ...   
</DiagnosticInformation>  
```  
  
## <a name="element-attributes"></a>元素属性  
  
|Attribute|描述|  
|---------------|-----------------|  
|**无**|N/A|  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|描述|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|每个 **ssbdiagnose** XML 输出文件一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|无。|  
|**子元素**|[Banner 元素 (ssbdiagnose)](../../tools/ssbdiagnose/banner-element-ssbdiagnose.md)<br /><br /> [Issue 元素 (ssbdiagnose)](../../tools/ssbdiagnose/issue-element-ssbdiagnose.md)|  
  
## <a name="remarks"></a>Remarks  
 有关 XML namespaces 的详细信息，请参阅 [MSDN Library 中的](http://go.microsoft.com/fwlink/?LinkId=7341) Namespaces in an XML Document [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
## <a name="see-also"></a>另请参阅  
 [ssbdiagnose 实用工具 (Service Broker)](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
