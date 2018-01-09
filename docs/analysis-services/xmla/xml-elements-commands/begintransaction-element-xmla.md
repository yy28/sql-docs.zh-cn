---
title: "BeginTransaction 元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: BeginTransaction Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#BeginTransaction
- microsoft.xml.analysis.begintransaction
- http://schemas.microsoft.com/analysisservices/2003/engine#BeginTransaction
helpviewer_keywords: BeginTransaction command
ms.assetid: fca122fc-b57c-4ba6-849b-ca8c93cf64e9
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e7ce11d146e54e2ee90c7944bc0ee27eb4f01175
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="begintransaction-element-xmla"></a>BeginTransaction 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]开始一项事务上与的实例的当前会话[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <BeginTransaction />  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 **BeginTransaction**命令开始在当前会话期间的活动事务。 如果存在活动事务，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例会递增当前会话的事务引用计数。 如果不存在活动事务，该实例将开始新的事务，并将当前会话的引用计数设置为 1。 如果使用显式指定的活动事务**BeginTransaction**命令时，显式指定事务内执行了所有后续命令。  
  
 如果当前会话结束，并且事务的引用计数大于零，则回滚所有的活动事务。  
  
 如果当前会话上不存在显式指定的活动事务，则在隐式定义的事务内执行从当前会话发出的所有命令。 如果命令成功执行，则提交隐式事务；如果命令失败，则回滚。  
  
## <a name="see-also"></a>另请参阅  
 [取消元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)   
 [CommitTransaction 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)   
 [RollbackTransaction 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)   
 [命令 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
