---
title: 为模型列创建别名 |Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e051c454223fc7fc710f45b97a1a76ecceb10f2b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62740218"
---
# <a name="create-an-alias-for-a-model-column"></a>为模型列创建别名
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，可以为模型列创建别名。 当挖掘结构名称太长而不便使用，或者当您需要重命名列以便更清楚地说明其内容或在模型中的用法时，这可能很有用。 例如，如果复制一个结构列，然后以不同的方式为特定模型离散化该列，可以重命名该列，以便更准确地反映其内容。  
  
 若要为模型列创建别名，请使用 **“属性”** 窗格并设置该列的 [“名称”](https://docs.microsoft.com/bi-reference/assl/properties/name-element-assl) 属性。  
  
 在数据挖掘设计器的 **“挖掘模型”** 选项卡上，别名显示在列用法标签旁的括号中。  
  
 有关如何在挖掘模型中设置属性的信息，请参阅 [挖掘模型列](../../analysis-services/data-mining/mining-model-columns.md)。  
  
### <a name="to-add-an-alias-to-a-mining-model-column"></a>为挖掘模型列添加别名  
  
1.  在数据挖掘设计器的“挖掘模型”  选项卡中，右键单击挖掘模型中与要更改的挖掘列对应的单元，然后选择“属性”  。  
  
2.  在屏幕右侧的 **“属性”** 窗口中，单击“名称”属性旁的单元格并删除当前值。 为该列键入一个新名称。  
  
## <a name="see-also"></a>请参阅  
 [挖掘模型任务和操作指南](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [挖掘模型属性](../../analysis-services/data-mining/mining-model-properties.md)  
  
  
