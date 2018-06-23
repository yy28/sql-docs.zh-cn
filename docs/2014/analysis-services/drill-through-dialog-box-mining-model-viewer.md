---
title: 钻取对话框 （挖掘模型查看器） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dm.miningmodeleditor.drillthrough.f1
ms.assetid: 42b78399-143d-4f44-90e0-b545ffb79e10
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: de01b0d081ecd26dc3472ebb697b72a42b128bab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026233"
---
# <a name="drill-through-dialog-box-mining-model-viewer"></a>“钻取”对话框（挖掘模型查看器）
  在使用数据挖掘设计器的 **“挖掘模型查看器”** 选项卡查看挖掘模型时，可以钻取到有关事例数据的详细信息（假定模型已启用钻取功能）。 而且，如果基础挖掘结构已启用钻取功能，则还可以查看挖掘结构中的列，即使挖掘模型中没有包含这些列也是如此。 在列列表中，结构列的前缀为标签 “Structure”。  
  
> [!NOTE]  
>  您不能对现有的挖掘结构启用钻取功能， 而必须重新创建挖掘结构并在创建过程中启用钻取功能。  
  
 有关如何从每个支持钻取，挖掘模型查看器中访问事例数据**请参阅**[钻取到用例数据从挖掘模型](data-mining/drill-through-to-case-data-from-a-mining-model.md)。  
  
## <a name="options"></a>“常规”  
 **事例分类为**  
 显示在选定的节点中包含的规则、项集和分类的定义。  
  
 **列列表**  
 显示模型中的列，后面跟随结构列。  
  
 **注意** 仅当对挖掘结构启用了钻取功能并且选中选项 **“模型和结构列”** 时才会显示结构列。 此外，您还必须具有对要查看列的挖掘模型和挖掘结构的钻取权限。  
  
 不包含在模型的结构列显示为**结构。\<列名称 >**。  
  
> [!NOTE]  
>  可在列网格中右键单击任意位置，并选择“全部复制”，以将钻取数据以制表符分隔的格式复制到剪贴板。 复制的数据只包含事例数据，而不包含节点定义。  
  
 **播放**  
 单击绿色箭头按钮刷新数据。  
  
## <a name="see-also"></a>请参阅  
 [钻取查询&#40;数据挖掘&#41;](data-mining/drillthrough-queries-data-mining.md)   
 [挖掘模型查看器&#40;数据挖掘模型设计器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [挖掘模型查看器任务和操作指南](data-mining/mining-model-viewer-tasks-and-how-tos.md)  
  
  