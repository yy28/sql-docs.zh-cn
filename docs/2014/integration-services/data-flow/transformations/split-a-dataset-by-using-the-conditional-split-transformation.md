---
title: 使用有条件拆分转换拆分数据集 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Conditional Split transformation
- splitting dataset
- datasets [Integration Services], splitting
ms.assetid: 23b3e84f-9296-4dc9-81c0-c7f06ae3f1ff
author: janinezhang
ms.author: janinez
ms.openlocfilehash: fc61f11a800a07a0b9a5ee1e9c3048a17bb36f13
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939266"
---
# <a name="split-a-dataset-by-using-the-conditional-split-transformation"></a>使用有条件拆分转换拆分数据集
  若要添加和配置有条件拆分转换，包必须已包含至少一个数据流任务和一个源。  
  
### <a name="to-conditionally-split-a-dataset"></a>有条件地拆分数据集  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“数据流”** 选项卡，并将有条件拆分转换从 **“工具箱”** 拖动到设计图面。  
  
4.  将连接器从数据源或前一个转换拖到有条件拆分转换，从而将有条件拆分转换连接到数据流。  
  
5.  双击有条件拆分转换。  
  
6.  在 **“有条件拆分转换编辑器”** 中，将变量、列、函数和运算符拖动到网格中的 **“条件”** 列，从而生成用作条件的表达式。 或者，也可以在 **“条件”** 列中键入表达式。  
  
    > [!NOTE]  
    >  变量或列可在多个表达式中使用。  
  
    > [!NOTE]  
    >  如果表达式无效，表达式文本将突出显示，列上的工具提示将对错误进行说明。  
  
7.  还可以在 **“输出名称”** 列中修改值。 默认名称为 Case 1、Case 2，依此类推。  
  
8.  若要修改计算条件的顺序，请单击向上箭头或向下箭头。  
  
    > [!NOTE]  
    >  将最可能遇到的条件放置在列表顶部。  
  
9. 对于不能匹配任何条件的数据行，如果需要，可以修改默认输出的名称。  
  
10. 若要配置错误输出，请单击 **“配置错误输出”** 。 有关详细信息，请参阅 [在数据流组件中配置错误输出](../../configure-an-error-output-in-a-data-flow-component.md)。  
  
11. 单击“确定”。   
  
12. 若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>另请参阅  
 [Conditional Split Transformation](conditional-split-transformation.md)   
 [Integration Services 转换](integration-services-transformations.md)   
 [Integration Services 路径](../integration-services-paths.md)   
 [Integration Services 数据类型](../integration-services-data-types.md)   
 [数据流任务](../../control-flow/data-flow-task.md)   
 [Integration Services (SSIS) 表达式](../../expressions/integration-services-ssis-expressions.md)  
  
  
