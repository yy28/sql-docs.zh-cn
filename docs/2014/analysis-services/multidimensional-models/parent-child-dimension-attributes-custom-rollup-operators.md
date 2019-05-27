---
title: 父子维度中的自定义汇总运算符 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- child rollup operations
- UnaryOperatorColumn property
- custom rollup operators [Analysis Services]
- unary operators
- parent-child dimensions [Analysis Services]
ms.assetid: a3ddd9fc-5fa3-4227-9322-8c45a5b5c2c3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 20f25474b15ecf58c45383a8290bb13f956a5db8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66073455"
---
# <a name="custom-rollup-operators-in-parent-child-dimensions"></a>父子维度中的自定义汇总运算符
  自定义汇总运算符提供了一种简单的方法，控制成员值如何汇总到父子层次结构的父值中。 在包含父子关系的维度中，可以指定包含一元运算符的列，以便用该运算符指定父属性的所有非计算成员的汇总。 计算出父成员的值后，一元运算符就将应用于成员。  
  
 一元运算符存储在由父属性的 `UnaryOperatorColumn` 属性所定义的列中，并且它们应用于属性的每个成员。 此属性所指定的列可以按维度表的外键驻留于维度表或与维度表相关的表中。  
  
 自定义汇总运算符提供了与自定义成员公式相似但比它更简化的功能。 自定义成员公式使用“多维表达式 (MDX)” 表达式确定汇总成员的方式。 相反，自定义汇总运算符使用简单的一元运算符确定成员的值如何影响父级。 在维度中，前面级别的自定义成员公式将覆盖某个级别的自定义汇总运算符。  
  
## <a name="custom-rollup-precedence"></a>自定义汇总优先级  
 在优先级方面，层次结构中某个级别的源属性的自定义汇总运算符将覆盖上一级的自定义成员公式。 而上一级的自定义成员公式将覆盖下一级的自定义汇总运算符。  
  
## <a name="see-also"></a>请参阅  
 [定义自定义成员公式](attribute-properties-define-custom-member-formulas.md)   
 [父子维度中的一元运算符](parent-child-dimension-attributes-unary-operators.md)  
  
  
