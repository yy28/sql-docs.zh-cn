---
title: 附加元素 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- Attach command
ms.assetid: a315d1f1-e220-4296-97cb-6d35606b9640
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eda22adcd9760fbeb01e009b0a8d9692f7e5d333
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48105397"
---
# <a name="attach-element"></a>附加元素
  将以前从当前服务器实例或另一个实例中分离的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库附加到当前服务器实例。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <Attach>  
      <Folder>...</Folder>  
            <ReadWriteMode>...</ReadWriteMode>  
            <Password>...</Password>  
   </Attach>  
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
|子元素|[文件夹](../xml-elements-properties/folder-element-xmla.md)<br /><br /> [ReadWriteMode](../xml-elements-properties/readwritemode-element.md)<br /><br /> [“密码”](../xml-elements-properties/password-element-xmla.md)|  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [分离元素](detach-element.md)   
 [附加和分离 Analysis Services 数据库](../../multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [移动 Analysis Services 数据库](../../multidimensional-models/move-an-analysis-services-database.md)   
 [数据库 Readwritemode](../../multidimensional-models/database-readwritemodes.md)   
 [切换 ReadOnly 和 ReadWrite 模式之间的 Analysis Services 数据库](../../multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  
