---
title: 父子维度中的自定义汇总运算符 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 000d6355aee1fc38aa4fdcb97cf02df2a4ef09da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68165424"
---
# <a name="parent-child-dimension-attributes---custom-rollup-operators"></a>父子维度特性 - 自定义汇总运算符
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  自定义汇总运算符提供了一种简单的方法，控制成员值如何汇总到父子层次结构的父值中。 在包含父子关系的维度中，可以指定包含一元运算符的列，以便用该运算符指定父属性的所有非计算成员的汇总。 计算出父成员的值后，一元运算符就将应用于成员。  
  
 一元运算符存储在由父属性的 **UnaryOperatorColumn** 属性所定义的列中，并且它们应用于属性的每个成员。 此属性所指定的列可以按维度表的外键驻留于维度表或与维度表相关的表中。  
  
 自定义汇总运算符提供了与自定义成员公式相似但比它更简化的功能。 自定义成员公式使用“多维表达式 (MDX)” 表达式确定汇总成员的方式。 相反，自定义汇总运算符使用简单的一元运算符确定成员的值如何影响父级。 在维度中，前面级别的自定义成员公式将覆盖某个级别的自定义汇总运算符。  
  
## <a name="custom-rollup-precedence"></a>自定义汇总优先级  
 在优先级方面，层次结构中某个级别的源属性的自定义汇总运算符将覆盖上一级的自定义成员公式。 而上一级的自定义成员公式将覆盖下一级的自定义汇总运算符。  
  
## <a name="see-also"></a>请参阅  
 [定义自定义成员公式](../../analysis-services/multidimensional-models/attribute-properties-define-custom-member-formulas.md)   
 [父子维度中的一元运算符](../../analysis-services/multidimensional-models/parent-child-dimension-attributes-unary-operators.md)  
  
  
