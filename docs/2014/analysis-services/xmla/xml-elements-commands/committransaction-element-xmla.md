---
title: CommitTransaction 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CommitTransaction Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#CommitTransaction
- urn:schemas-microsoft-com:xml-analysis#CommitTransaction
- microsoft.xml.analysis.committransaction
helpviewer_keywords:
- CommitTransaction command
ms.assetid: 1cd814dc-a0be-4305-b44d-faf15e843f7d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eff18a85bc33dfc47377f0613f0696811ff1389a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203197"
---
# <a name="committransaction-element-xmla"></a>CommitTransaction 元素 (XMLA)
  提交事务在当前会话[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <CommitTransaction />  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `CommitTransaction` 命令提交在当前会话上使用 `BeginTransaction` 元素显式定义的活动事务。 如果不存在活动事务，则会出现错误。 如果存在活动事务，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例会减小当前会话的事务引用计数。 如果显式定义的活动事务的引用计数减到零，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例将提交该事务。  
  
## <a name="see-also"></a>请参阅  
 [BeginTransaction 元素&#40;XMLA&#41;](begintransaction-element-xmla.md)   
 [Cancel 元素&#40;XMLA&#41;](cancel-element-xmla.md)   
 [RollbackTransaction 元素&#40;XMLA&#41;](rollbacktransaction-element-xmla.md)   
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
