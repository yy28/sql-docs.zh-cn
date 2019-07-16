---
title: 级别属性-用户层次结构 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 230ec186562c99b2851c18e910474c207698d300
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209215"
---
# <a name="user-hierarchies---level-properties"></a>用户层次结构 - 级别属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  下表列出了用户定义层次结构中的一个级别的属性并对其进行了说明。  
  
|属性|描述|  
|--------------|-----------------|  
|描述|包含对级别的说明。|  
|HideMemberIf|指示是否应该从客户端应用程序中隐藏某一级别的成员以及何时隐藏。 此属性可以有下列值：<br /><br /> 从不<br /> 从不隐藏成员。 这是默认值。<br /><br /> OnlyChildWithNoName<br /> 当成员是其父级的唯一子级并且成员名称为空时，隐藏该成员。<br /><br /> OnlyChildWithParentName<br /> 当成员是其父级的唯一子级并且成员名称与其父级的名称相同时，隐藏该成员。<br /><br /> NoName<br /> 当成员的名称为空时，隐藏该成员。<br /><br /> ParentName<br /> 当成员的名称与其父级的名称相同时，隐藏该成员。|  
|id|包含级别的唯一标识符 (ID)。|  
|名称|包含级别的友好名称。 默认情况下，级别的名称与源属性的名称相同。|  
|SourceAttribute|包含级别所基于的源属性的名称。|  
  
## <a name="see-also"></a>请参阅  
 [用户层次结构属性](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)  
  
  
