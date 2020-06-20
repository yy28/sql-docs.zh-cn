---
title: 在数据流组件中使用表达式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], data flow
- expressions [Integration Services], data flow components
ms.assetid: 9181b998-d24a-41fb-bb3c-14eee34f910d
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d08d256946fbeb2f5b70057fc0d6992758b3a211
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972627"
---
# <a name="use-an-expression-in-a-data-flow-component"></a>在数据流组件中使用表达式
  本过程介绍如何将表达式添加到有条件拆分转换或派生列转换中。 有条件拆分转换使用表达式定义将数据行定向到转换输出的条件，而派生列转换使用表达式定义分配给列的值。  
  
 若要在转换中实现表达式，包必须至少已经包含一项数据流任务和一个源。 有关将项添加到包中的信息，请参阅以下主题：  
  
-   [在控制流中添加或删除任务或容器](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
    
  
-   [在数据流中添加或删除组件](data-flow/add-or-delete-a-component-in-a-data-flow.md)  
  
-   [连接数据流中的组件](data-flow/connect-components-in-a-data-flow.md)  
  
### <a name="to-create-an-expression"></a>创建表达式  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中，单击 **“控制流”** 选项卡，然后单击包含要在其中实现表达式的数据流的数据流任务。  
  
4.  单击 **“数据流”** 选项卡，然后将有条件拆分转换或派生列转换从 **“工具箱”** 拖到设计图面。  
  
5.  将绿色的连接器从源或转换拖到有条件拆分转换或派生列转换。  
  
6.  双击该转换打开其对话框。  
  
7.  在左窗格中，展开“变量”显示系统变量和用户定义的变量，然后展开“列”显示转换输入列。********  
  
8.  在右窗格中，展开“数学函数”、“字符串函数”、“日期/时间函数”、“NULL 函数”、“类型转换”和“运算符”，访问表达式语法提供的函数、转换和运算符。************************  
  
9. 根据转换的类型，可以执行下列某项操作来生成表达式：  
  
    -   在 **“有条件拆分转换编辑器”** 对话框中，将变量、列、函数、运算符和转换拖到 **“条件”** 列中。 另外，您还可以直接在 **“条件”** 列中键入表达式。  
  
    -   在 **“派生列转换编辑器”** 对话框中，将变量、列、函数、运算符和转换拖到 **“表达式”** 列中。 另外，您还可以直接在 **“表达式”** 列中键入表达式。  
  
        > [!NOTE]  
        >   当焦点离开 **“条件”** 列或 **“表达式”** 列时，表达式文本可能会突出显示，指示表达式语法不正确。  
  
10. 单击 **“确定”**，退出对话框。  
  
    > [!NOTE]  
    >  如果该表达式无效，则会出现一个警告，描述表达式中的语法错误。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services &#40;SSIS&#41; 表达式](expressions/integration-services-ssis-expressions.md)   
 [有条件拆分转换](data-flow/transformations/conditional-split-transformation.md)   
 [派生列转换](data-flow/transformations/derived-column-transformation.md)   
 [数据流任务](control-flow/data-flow-task.md)   
 数据流  
  
  
