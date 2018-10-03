---
title: ClearCache 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ClearCache Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#ClearCache
- urn:schemas-microsoft-com:xml-analysis#ClearCache
- microsoft.xml.analysis.clearcache
helpviewer_keywords:
- ClearCache command
ms.assetid: e154b489-e443-469a-9490-43c62da62e11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b5bcc8840d57f4290ef0d0cf70908f0c75921bcf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48084387"
---
# <a name="clearcache-element-xmla"></a>ClearCache 元素 (XMLA)
  在清除指定的对象的内存缓存[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <ClearCache>  
      <Object>...</Object>  
   </ClearCache>  
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
|子元素|[对象](../xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>备注  
 `ClearCache`命令可刷新的缓存指定的数据库、 维度、 多维数据集、 度量值组或分区上[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。 如果在 `Object` 元素中指定了一个对象，而不是数据库、维度、多维数据集、度量值组或分区，则会出错。  
  
## <a name="see-also"></a>请参阅  
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
