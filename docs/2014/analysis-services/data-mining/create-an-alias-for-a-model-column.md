---
title: 为模型列创建别名 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], how-to topics
- mining models [Analysis Services], columns
- column names [Analysis Services]
ms.assetid: c80ebe66-a8f8-4f24-9fe8-8288de9d13bc
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: cf049cdd7fabbc50fdacf5ab72ca3ce1845482f7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027114"
---
# <a name="create-an-alias-for-a-model-column"></a>为模型列创建别名
  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，可以为模型列创建别名。 当挖掘结构名称太长而不便使用，或者当您需要重命名列以便更清楚地说明其内容或在模型中的用法时，这可能很有用。 例如，如果复制一个结构列，然后以不同的方式为特定模型离散化该列，可以重命名该列，以便更准确地反映其内容。  
  
 若要为模型列创建别名，请使用 **“属性”** 窗格并设置该列的 [“名称”](../scripting/properties/name-element-assl.md) 属性。  
  
 在数据挖掘设计器的 **“挖掘模型”** 选项卡上，别名显示在列用法标签旁的括号中。  
  
 有关如何在挖掘模型中设置属性的信息，请参阅 [挖掘模型列](mining-model-columns.md)。  
  
### <a name="to-add-an-alias-to-a-mining-model-column"></a>为挖掘模型列添加别名  
  
1.  在数据挖掘设计器的“挖掘模型”选项卡中，右键单击挖掘模型中与要更改的挖掘列对应的单元，然后选择“属性”。  
  
2.  在屏幕右侧的 **“属性”** 窗口中，单击“名称”属性旁的单元格并删除当前值。 为该列键入一个新名称。  
  
## <a name="see-also"></a>请参阅  
 [挖掘模型任务和操作指南](mining-model-tasks-and-how-tos.md)   
 [挖掘模型属性](mining-model-properties.md)  
  
  