---
title: "删除元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Delete Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.delete
- urn:schemas-microsoft-com:xml-analysis#Delete
- http://schemas.microsoft.com/analysisservices/2003/engine#Delete
helpviewer_keywords:
- Delete element
ms.assetid: 76201b18-11e9-4815-9287-27a068d8fbc5
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 49ba01a51b67841f96ff2bea3b6a516cf38484a9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="delete-element-xmla"></a>Delete 元素 (XMLA)
  删除对象上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <Delete IgnoreFailures="boolean">  
      <Object>...</Object>  
   </Delete>  
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
|子元素|[对象](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="attributes"></a>属性  
  
|Attribute|说明|  
|---------------|-----------------|  
|IgnoreFailures|可选的 **Boolean** 属性。 如果设置为 True，则 **Execute** 方法将忽略网络故障或与远程分区相关的故障。|  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [命令 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  

