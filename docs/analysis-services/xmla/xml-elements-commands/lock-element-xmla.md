---
title: 锁定元素 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Lock Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Lock
- microsoft.xml.analysis.lock
- http://schemas.microsoft.com/analysisservices/2003/engine#Lock
helpviewer_keywords:
- Lock command
ms.assetid: a819e805-4793-43bb-8af3-16a19f8bdab3
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 98e5087dc10ae495dec711c35fa807cb9fd68e02
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="lock-element-xmla"></a>Lock 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]锁定指定的对象上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <Lock>  
      <ID>...</ID>  
      <Object>...</Object>  
      <Mode>...</Mode>  
   </Lock>  
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
|子元素|[ID](../../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md)，[模式](../../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md)，[对象](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 **锁**命令锁定的对象，供共享或独占使用，在当前活动事务的上下文中。 只有数据库管理员或服务器管理员可以显式发出**锁**命令。 对象上的锁将阻止提交事务，直到删除该锁为止。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 支持两种类型的锁：共享锁和排他锁。 有关支持的锁类型的详细信息[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，请参阅[模式元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md).  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 仅允许锁定数据库。 **对象**元素必须包含对的对象引用[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库。 如果**对象**未指定元素或如果**对象**元素引用数据库之外的对象将会出错。  
  
 其他的隐式命令问题**锁**命令[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库。 从数据库，如任何中读取数据或元数据的任何操作**发现**方法或**执行**运行方法**语句**命令，隐式颁发共享锁定数据库上。 将数据或元数据中的更改提交到一个对象，在任何事务[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库，如**执行**运行方法**Alter**命令，隐式上发出的排他锁数据库。  
  
 所有锁都位于当前事务的上下文中。 当提交或回滚当前事务时，事务中定义的所有锁都将自动释放。  
  
## <a name="see-also"></a>另请参阅  
 [解锁元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)   
 [命令 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
