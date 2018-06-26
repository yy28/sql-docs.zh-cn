---
title: 使用合并联接转换扩展数据集 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Merge Join transformation
- datasets [Integration Services], joining
- datasets [Integration Services], extending
- joining datasets [Integration Services]
ms.assetid: 9e512c3c-f89b-45f3-8281-cdb8f35a2b1f
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 27d88e5105ddbbdbc8e9f8b5826b658921db2a1f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024867"
---
# <a name="extend-a-dataset-by-using-the-merge-join-transformation"></a>使用合并联接转换扩展数据集
  若要添加和配置合并联接转换，则包中必须已包含至少一个数据流任务和为合并联接转换提供输入的两个数据流组件。  
  
 合并联接转换需要两个已排序的输入。 有关详细信息，请参阅 [为合并转换和合并联接转换排序数据](sort-data-for-the-merge-and-merge-join-transformations.md)。  
  
### <a name="to-extend-a-dataset"></a>扩展数据集  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“数据流”** 选项卡，然后从 **“工具箱”** 中将合并联接转换拖动到设计图面上。  
  
4.  将连接线从数据源或前一个转换拖到合并联接转换，从而将合并联接转换连接到数据流。  
  
5.  双击合并联接转换。  
  
6.  在 **“合并联接转换编辑器”** 对话框的 **“联接类型”** 列表中，选择要用的联接类型。  
  
    > [!NOTE]  
    >  如果选择了“左外部联接”类型，那么可以单击“交换输入”来切换输入，将左外部联接转换为右外部联接。  
  
7.  将左输入中的列拖动到右输入中的列，以指定联接列。 如果这些列名称相同，则可以选中 **“联接键”** 复选框，合并联接转换将自动创建联接。  
  
    > [!NOTE]  
    >  只能在具有相同排序位置的列之间创建联接，而且必须按照排序位置所指定的顺序创建联接。 如果尝试不按顺序创建联接， **“合并联接转换编辑器”** 会提示您为跳过的排序顺序位置创建其他联接。  
  
    > [!NOTE]  
    >  默认情况下，输出根据联接列进行排序。  
  
8.  在左输入和右输入中，选中要包含在输出中的其他列的复选框。 默认情况下包含联接列。  
  
9. 还可以更新 **“输出别名”** 列中的输出列名称。  
  
10. 单击“确定” 。  
  
11. 若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>请参阅  
 [合并联接转换](merge-join-transformation.md)   
 [Integration Services 转换](integration-services-transformations.md)   
 [Integration Services 路径](../integration-services-paths.md)   
 [数据流任务]((../../control-flow/data-flow-task.md)  
  
  