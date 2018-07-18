---
title: MDX 语法元素 (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3c976cd33e73828698eac0ac43b5cd6878ac36b0
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742236"
---
# <a name="mdx-syntax-elements-mdx"></a>MDX 语法元素 (MDX)


  多维表达式 (MDX) 具有一些由大多数语句使用或受其影响的元素：  
  
|术语|定义|  
|----------|----------------|  
|[标识符](../mdx/identifiers-mdx.md)|标识符是对象（如多维数据集、维度、成员和度量值）的名称。|  
|**数据类型**|定义单元、成员属性和单元属性中包含的数据的类型。 MDX 只支持 OLE VARIANT 数据类型。 有关 VARIANT 数据类型的强制、转换和操作的详细信息，请参阅 Platform SDK 文档中的“VARIANT 和 VARIANTARG”。|  
|[表达式&#40;MDX&#41;](../mdx/expressions-mdx.md)|表达式是语法的 Analysis Services 可以解析为单个 （标量） 值或对象的单元。 表达式包含返回单个值、集表达式等的函数。|  
|[运算符](../mdx/operators-mdx-syntax.md)|运算符是与一个或多个简单的 MDX 表达式一起使用、以构成更复杂的 MDX 表达式的语法元素。|  
|[函数](../mdx/functions-mdx-syntax.md)|函数是可以接受零个、一个或多个输入值并返回一个标量值或对象的语法元素。 示例包括[总和](../mdx/sum-mdx.md)添加多个值，函数[成员](../mdx/members-set-mdx.md)函数返回一组的成员从维度或级别上，依次类推。|  
|[注释](../mdx/comments-mdx-syntax.md)|注释是插入到 MDX 语句或脚本中，用来说明语句用途的文本段。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不会执行注释。|  
|[保留关键字](../mdx/reserved-keywords-mdx-syntax.md)|保留关键字是保留起来供 MDX 使用，且不应用作 MDX 语句中使用的对象名称的关键字。|  
|[成员、 元组和集](../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)|成员、元组和集是创建 MDX 查询之前必须了解的多维数据的核心概念。|  
  
## <a name="see-also"></a>请参阅  
 [多维表达式&#40;MDX&#41;引用](../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
