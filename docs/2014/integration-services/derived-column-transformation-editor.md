---
title: 派生列转换编辑器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.derivedcolumntransformation.f1
helpviewer_keywords:
- Derived Column Transformation Editor
ms.assetid: ff73923e-d245-43d8-bf24-af3bdc942e51
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4fc2701ad53cd0071be40100d168d5d5571d2958
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66059572"
---
# <a name="derived-column-transformation-editor"></a>派生列转换编辑器
  可以使用 **“派生列转换编辑器”** 对话框，创建填充新列或替换列的表达式。  
  
 若要了解有关派生列转换的详细信息，请参阅 [Derived Column Transformation](data-flow/transformations/derived-column-transformation.md)。  
  
## <a name="options"></a>选项  
 **变量和列**  
 通过将变量或输入列从可用变量和列的列表中拖到下面窗格中的现有表行，或者拖到列表底部的新行中，生成使用变量或输入列的表达式。  
  
 **函数和运算符**  
 通过将函数和运算符从列表中拖到下面的窗格中，生成使用函数或运算符的表达式，以计算输入数据和直接输出数据。  
  
 **派生列名称**  
 提供派生列名称。 默认值为带编号的派生列列表；不过，您也可以任选一个唯一的描述性名称。  
  
 **派生列**  
 从列表中选择派生列。 选择是将派生列添加为新的输出列，还是替换现有列中的数据。  
  
 **表达式**  
 键入表达式，或通过从可用列、变量、函数和运算符的以前列表中进行拖动来生成表达式。  
  
 此属性的值可以使用属性表达式来指定。  
  
 **相关主题**：[Integration Services &#40;SSIS&#41; 表达式](expressions/integration-services-ssis-expressions.md)、[运算符（SSIS 表达式）](expressions/operators-ssis-expression.md)和[函数（SSIS 表达式）](expressions/functions-ssis-expression.md)  
  
 **数据类型**  
 如果向新列中添加数据，“派生列转换编辑器”对话框将自动计算表达式的值并设置相应的数据类型。 该列的值是只读的。 有关详细信息，请参阅 [Integration Services 数据类型](data-flow/integration-services-data-types.md)。  
  
 **长度**  
 如果向新列中添加数据，“派生列转换编辑器”对话框将自动计算表达式的值并设置字符串数据的列长度。 该列的值是只读的。  
  
 **精度**  
 如果向新列中添加数据，“派生列转换编辑器”对话框将自动根据数据类型来设置数值数据的精度。 该列的值是只读的。  
  
 **小数位数**  
 如果向新列中添加数据，“派生列转换编辑器”对话框将自动根据数据类型来设置数值数据的小数位数。 该列的值是只读的。  
  
 **代码页**  
 如果向新列中添加数据，“派生列转换编辑器”对话框将自动设置 DT_STR 数据类型的代码页。 可以更新 **“代码页”**。  
  
 **配置错误输出**  
 使用 [配置错误输出](../../2014/integration-services/configure-error-output.md) 对话框指定处理错误的方式。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [使用派生列转换派生列值](data-flow/transformations/derive-column-values-by-using-the-derived-column-transformation.md)  
  
  
