---
title: 级别属性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
ms.assetid: dabb7335-887b-442a-b67c-4901ba1242b7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1edce09247d89b8b87c8d03a637f84ed42e2292c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075117"
---
# <a name="level-properties"></a>级别属性 
  下表列出了用户定义层次结构中的一个级别的属性并对其进行了说明。  
  
|“属性”|Description|  
|--------------|-----------------|  
|Description|包含对级别的说明。|  
|HideMemberIf|指示是否应该从客户端应用程序中隐藏某一级别的成员以及何时隐藏。 此属性可以有下列值：<br /><br /> 从不<br /> 从不隐藏成员。 这是默认值。<br /><br /> OnlyChildWithNoName<br /> 当成员是其父级的唯一子级并且成员名称为空时，隐藏该成员。<br /><br /> OnlyChildWithParentName<br /> 当成员是其父级的唯一子级并且成员名称与其父级的名称相同时，隐藏该成员。<br /><br /> NoName<br /> 当成员的名称为空时，隐藏该成员。<br /><br /> ParentName<br /> 当成员的名称与其父级的名称相同时，隐藏该成员。|  
|ID|包含级别的唯一标识符 (ID)。|  
|“属性”|包含级别的友好名称。 默认情况下，级别的名称与源属性的名称相同。|  
|SourceAttribute|包含级别所基于的源属性的名称。|  
  
## <a name="see-also"></a>请参阅  
 [用户层次结构属性](user-hierarchies-properties.md)  
  
  
