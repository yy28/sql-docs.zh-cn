---
title: "父子维度中的自定义汇总运算符 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- child rollup operations
- UnaryOperatorColumn property
- custom rollup operators [Analysis Services]
- unary operators
- parent-child dimensions [Analysis Services]
ms.assetid: a3ddd9fc-5fa3-4227-9322-8c45a5b5c2c3
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 328bd8977389ac39d049d44095c447a2843efdbe
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="parent-child-dimension-attributes---custom-rollup-operators"></a>父-子维度属性的自定义汇总运算符
  自定义汇总运算符提供了一种简单的方法，控制成员值如何汇总到父子层次结构的父值中。 在包含父子关系的维度中，可以指定包含一元运算符的列，以便用该运算符指定父属性的所有非计算成员的汇总。 计算出父成员的值后，一元运算符就将应用于成员。  
  
 一元运算符存储在由父属性的 **UnaryOperatorColumn** 属性所定义的列中，并且它们应用于属性的每个成员。 此属性所指定的列可以按维度表的外键驻留于维度表或与维度表相关的表中。  
  
 自定义汇总运算符提供了与自定义成员公式相似但比它更简化的功能。 自定义成员公式使用“多维表达式 (MDX)” 表达式确定汇总成员的方式。 相反，自定义汇总运算符使用简单的一元运算符确定成员的值如何影响父级。 在维度中，前面级别的自定义成员公式将覆盖某个级别的自定义汇总运算符。  
  
## <a name="custom-rollup-precedence"></a>自定义汇总优先级  
 在优先级方面，层次结构中某个级别的源属性的自定义汇总运算符将覆盖上一级的自定义成员公式。 而上一级的自定义成员公式将覆盖下一级的自定义汇总运算符。  
  
## <a name="see-also"></a>另请参阅  
 [定义自定义成员公式](../../analysis-services/multidimensional-models/attribute-properties-define-custom-member-formulas.md)   
 [父子维度中的一元运算符](../../analysis-services/multidimensional-models/parent-child-dimension-attributes-unary-operators.md)  
  
  

