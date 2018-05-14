---
title: 锁定元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1c70794517988229691c6336db412263cbfa721f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="lock-element-xmla"></a>Lock 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  锁定指定的对象上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[ID](../../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md), [Mode](../../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md), [Object](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 **锁**命令锁定的对象，供共享或独占使用，在当前活动事务的上下文中。 只有数据库管理员或服务器管理员可以显式发出**锁**命令。 对象上的锁将阻止提交事务，直到删除该锁为止。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 支持两种类型的锁：共享锁和排他锁。 有关支持的锁类型的详细信息[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，请参阅[模式元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md).  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 仅允许锁定数据库。 **对象**元素必须包含对的对象引用[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库。 如果**对象**未指定元素或如果**对象**元素引用数据库之外的对象将会出错。  
  
 其他的隐式命令问题**锁**命令[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库。 从数据库，如任何中读取数据或元数据的任何操作**发现**方法或**执行**运行方法**语句**命令，隐式颁发共享锁定数据库上。 将数据或元数据中的更改提交到一个对象，在任何事务[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库，如**执行**运行方法**Alter**命令，隐式上发出的排他锁数据库。  
  
 所有锁都位于当前事务的上下文中。 当提交或回滚当前事务时，事务中定义的所有锁都将自动释放。  
  
## <a name="see-also"></a>另请参阅  
 [解锁元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)   
 [命令 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
