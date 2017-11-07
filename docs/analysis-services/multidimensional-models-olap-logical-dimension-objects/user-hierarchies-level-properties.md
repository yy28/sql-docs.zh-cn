---
title: "级别属性-用户层次结构 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
ms.assetid: dabb7335-887b-442a-b67c-4901ba1242b7
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7fa44b453e1c91d8a43dde01ec582b59f22d3824
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="user-hierarchies---level-properties"></a>用户层次结构的级别的属性
  下表列出了用户定义层次结构中的一个级别的属性并对其进行了说明。  
  
|属性|Description|  
|--------------|-----------------|  
|Description|包含对级别的说明。|  
|HideMemberIf|指示是否应该从客户端应用程序中隐藏某一级别的成员以及何时隐藏。 此属性可以有下列值：<br /><br /> 从不<br /> 从不隐藏成员。 这是默认值。<br /><br /> OnlyChildWithNoName<br /> 当成员是其父级的唯一子级并且成员名称为空时，隐藏该成员。<br /><br /> OnlyChildWithParentName<br /> 当成员是其父级的唯一子级并且成员名称与其父级的名称相同时，隐藏该成员。<br /><br /> NoName<br /> 当成员的名称为空时，隐藏该成员。<br /><br /> ParentName<br /> 当成员的名称与其父级的名称相同时，隐藏该成员。|  
|ID|包含级别的唯一标识符 (ID)。|  
|名称|包含级别的友好名称。 默认情况下，级别的名称与源属性的名称相同。|  
|SourceAttribute|包含级别所基于的源属性的名称。|  
  
## <a name="see-also"></a>另请参阅  
 [用户层次结构属性](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)  
  
  

