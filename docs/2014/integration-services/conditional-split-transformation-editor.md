---
title: 有条件拆分转换编辑器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.conditionalsplittransformation.f1
helpviewer_keywords:
- Conditional Split Transformation Editor
ms.assetid: c30e1633-537a-4837-9991-6203c6f2a21e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 920ec41ae30d53853cfb757fb7fc33610953dc86
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66060884"
---
# <a name="conditional-split-transformation-editor"></a>有条件拆分转换编辑器
  可以使用 **“有条件拆分转换编辑器”** 对话框创建表达式，设置表达式计算顺序，以及对有条件拆分输出进行命名。 此对话框包含可以用于生成表达式的数学、字符串和日期/时间函数及运算符。 计算结果为 True 的第一个条件确定了行定向到的输出。  
  
> [!NOTE]  
>  有条件拆分转换仅将每个输入行定向到一个输出。 如果输入多个条件，则转换会将每一行发送到条件为 True 的第一个输出，而忽略各行的后续条件。 如果需要连续计算多个条件，则可能需要在数据流中连接多个有条件拆分转换。  
  
 若要了解有关有条件拆分转换的详细信息，请参阅 [有条件拆分转换](data-flow/transformations/conditional-split-transformation.md)。  
  
## <a name="options"></a>选项  
 **订单**  
 选择行并使用右边的箭头键，可以更改计算表达式的顺序。  
  
 **输出名称**  
 提供输出名称。 默认为带编号的名称示例列表，不过，您也可以任选一个唯一的描述性名称。  
  
 **条件**  
 键入表达式，或通过从可用的列、变量、函数和运算符的列表中拖动相应项来生成表达式。  
  
 此属性的值可以使用属性表达式来指定。  
  
 **相关主题：**[Integration Services &#40;SSIS&#41; 表达式](expressions/integration-services-ssis-expressions.md)、[运算符（SSIS 表达式）](expressions/operators-ssis-expression.md)和[函数（SSIS 表达式）](expressions/functions-ssis-expression.md)  
  
 **默认输出名称**  
 为默认输出键入名称，或使用默认名称。  
  
 **配置错误输出**  
 使用 [配置错误输出](../../2014/integration-services/configure-error-output.md) 对话框指定处理错误的方式。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [使用有条件拆分转换拆分数据集](data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
  
