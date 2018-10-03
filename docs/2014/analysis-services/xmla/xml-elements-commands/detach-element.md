---
title: 分离元素 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- Detach command
ms.assetid: adbc7920-2a4a-4842-9e6f-37006fa19ff8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b3255af420e600f2197cdf7ecb8d76cc2f879e61
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48097440"
---
# <a name="detach-element"></a>分离元素
  将 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库从当前服务器实例中分离。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <Detach>  
      <Object>...</Object>  
      <Password>...</Password>  
   </Detach>  
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
|子元素|[对象](../xml-elements-properties/object-element-xmla.md)<br /><br /> [“密码”](../xml-elements-properties/password-element-xmla.md)|  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [附加元素](attach-element.md)   
 [附加和分离 Analysis Services 数据库](../../multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [移动 Analysis Services 数据库](../../multidimensional-models/move-an-analysis-services-database.md)   
 [数据库 Readwritemode](../../multidimensional-models/database-readwritemodes.md)   
 [切换 ReadOnly 和 ReadWrite 模式之间的 Analysis Services 数据库](../../multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  
