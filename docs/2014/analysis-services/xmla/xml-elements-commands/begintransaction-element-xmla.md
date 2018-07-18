---
title: BeginTransaction 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- BeginTransaction Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#BeginTransaction
- microsoft.xml.analysis.begintransaction
- http://schemas.microsoft.com/analysisservices/2003/engine#BeginTransaction
helpviewer_keywords:
- BeginTransaction command
ms.assetid: fca122fc-b57c-4ba6-849b-ca8c93cf64e9
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1685c1c61c248cf37672cab17ccf3144e7d5e7ec
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37253039"
---
# <a name="begintransaction-element-xmla"></a>BeginTransaction 元素 (XMLA)
  实例的当前会话上开始一个事务[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
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
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `BeginTransaction` 命令在当前会话上开始一个活动事务。 如果存在活动事务，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例会递增当前会话的事务引用计数。 如果不存在活动事务，该实例将开始新的事务，并将当前会话的引用计数设置为 1。 如果使用 `BeginTransaction` 命令显式指定一个活动事务，则会在显式指定的事务内执行所有后续命令。  
  
 如果当前会话结束，并且事务的引用计数大于零，则回滚所有的活动事务。  
  
 如果当前会话上不存在显式指定的活动事务，则在隐式定义的事务内执行从当前会话发出的所有命令。 如果命令成功执行，则提交隐式事务；如果命令失败，则回滚。  
  
## <a name="see-also"></a>请参阅  
 [Cancel 元素&#40;XMLA&#41;](cancel-element-xmla.md)   
 [CommitTransaction 元素&#40;XMLA&#41;](committransaction-element-xmla.md)   
 [RollbackTransaction 元素&#40;XMLA&#41;](rollbacktransaction-element-xmla.md)   
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
