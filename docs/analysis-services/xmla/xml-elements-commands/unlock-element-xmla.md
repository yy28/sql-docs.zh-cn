---
title: Unlock 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfilee"
ms.openlocfilehash: eb9cced037ab7fcf7072e6db56cb645333a02311
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="unlock-element-xmla"></a>Unlock 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  将指定的锁解锁上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <Unlock>  
      <ID>...</ID>  
   </Unlock>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[ID](../../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 **Unlock** 命令可删除在当前活动事务的上下文中建立的锁。 只有数据库管理员或服务器管理员可以显式发出 **Unlock** 命令。  
  
 所有锁都位于当前事务的上下文中。 当提交或回滚当前事务时，事务中定义的所有锁都将自动释放。  
  
## <a name="see-also"></a>另请参阅  
 [锁定元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)   
 [命令 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
