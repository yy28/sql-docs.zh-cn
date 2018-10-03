---
title: 锁定元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Lock Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Lock
- microsoft.xml.analysis.lock
- http://schemas.microsoft.com/analysisservices/2003/engine#Lock
helpviewer_keywords:
- Lock command
ms.assetid: a819e805-4793-43bb-8af3-16a19f8bdab3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aee5d603c2708cb42b666d3cc0c9acc5ea208f0b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079517"
---
# <a name="lock-element-xmla"></a>Lock 元素 (XMLA)
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[ID](../xml-elements-properties/id-element-xmla.md)，[模式](../xml-elements-properties/mode-element-xmla.md)，[对象](../xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>备注  
 `Lock` 命令锁定当前活动事务上下文中的对象，该锁可为共享锁或排他锁。 只有数据库管理员或服务器管理员可以显式发出 `Lock` 命令。 对象上的锁将阻止提交事务，直到删除该锁为止。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 支持两种类型的锁：共享锁和排他锁。 有关支持的锁类型的详细信息[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，请参阅[Mode 元素&#40;XMLA&#41;](../xml-elements-properties/mode-element-xmla.md)。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 仅允许锁定数据库。 `Object` 元素必须包含对 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库的对象引用。 如果未指定 `Object` 元素或 `Object` 元素引用数据库以外的对象，则将引发错误。  
  
 其他命令将对 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库隐式发出 `Lock` 命令。 任何从数据库读取数据或元数据的操作，例如任何运行 `Discover` 命令的 `Execute` 方法或 `Statement` 方法将对数据库隐式发出一个共享锁。 任何提交对 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库上对象的数据更改或元数据更改的事务，例如运行 `Execute` 命令的 `Alter` 方法，将对数据库隐式发出一个排他锁。  
  
 所有锁都位于当前事务的上下文中。 当提交或回滚当前事务时，事务中定义的所有锁都将自动释放。  
  
## <a name="see-also"></a>请参阅  
 [Unlock 元素&#40;XMLA&#41;](lock-element-xmla.md)   
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
