---
title: 父子维度中的一元运算符 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UnaryOperatorColumn property
- attributes [Analysis Services], unary operators
- unary operators
ms.assetid: b8ef549c-5458-458a-bf1a-fd743a1417fd
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c5837a9c1c19b6bf571948ca7d30a862ce41f9d8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014188"
---
# <a name="unary-operators-in-parent-child-dimensions"></a>父子维度中的一元运算符
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中包含父子关系的维度中，可以为父属性的所有非计算成员指定将确定其自定义汇总的一元（或自定义汇总）运算符列。 计算出父成员的值后，一元运算符就将应用于成员。 父属性中的 **UnaryOperatorColumn** (**Usage**=Parent) 指定了数据源视图中包含一元运算符的表列。 存储在此列中的自定义汇总运算符的值将应用于属性的每个成员。  
  
 可以在数据源视图的维度表中创建和指定作为一元运算符列的命名计算。 最简单的表达式（如“+”）对所有成员都将返回相同的运算符。 但是，可以使用任何表达式，只要它为每个成员都返回运算符。  
  
 可以在父属性中手动更改 **UnaryOperatorColumn** 属性设置，也可以使用商业智能向导的“定义自定义聚合”增强功能替换与维度成员关联的默认聚合。 有关如何使用商业智能向导执行此配置的详细信息，请参阅 [向维度中添加自定义聚合](bi-wizard-add-a-custom-aggregation-to-a-dimension.md)。  
  
 父属性的 **UnaryOperatorColumn** 属性的默认设置是“(none)”，它表示禁用自定义汇总运算符。 下表列出了一元运算符，并说明了将它们应用于某个级别时它们的行为。  
  
|一元运算符|Description|  
|--------------------|-----------------|  
|+（加号）|成员的值将添加到在该成员之前发生的同级成员的聚合值中。 如果没有为属性定义一元运算符列，那么，这是默认运算符。|  
|-（减号）|从成员之前发生的同级成员的聚合值中减去该成员的值。|  
|*（星号）|成员的值乘以在该成员之前发生的同级成员的聚合值。|  
|/（斜杠）|成员的值除以在该成员之前发生的同级成员的聚合值。|  
|~（代字号）|忽略成员的值。|  
  
 空值和在表中没找到的其他值将被视为使用加号 (+) 一元运算符。 因为没有运算符优先级，所以成员在一元运算符列存储的顺序决定了求值的顺序。 若要更改求值的顺序，请创建新的特性，并将其“类型”  属性设置为“顺序” ，然后在其“源列”  属性中分配对应于求值顺序的顺序号。 还必须按该属性对属性的成员排序。 有关如何使用商业智能向导对属性成员排序的信息，请参阅 [定义维度的排序](bi-wizard-define-the-ordering-for-a-dimension.md)。  
  
 可以使用 **UnaryOperatorColumn** 属性指定一个命名计算，以返回一元运算符作为该属性的所有成员的文字字符。 此操作就像在命名计算中键入文字字符（例如， `'*'` ）一样简单。 这会对属性的所有成员用乘法运算符（星号 (*)）来替换默认的运算符（加号 (+)）。 有关详细信息，请参阅[在数据源视图中定义命名计算 (Analysis Services)](define-named-calculations-in-a-data-source-view-analysis-services.md)。  
  
 在维度设计器的 **“浏览器”** 选项卡中，可以查看层次结构中每个成员旁边的一元运算符。 还可以在处理启用写入的维度时更改一元运算符。 如果维度没有启用写入，则必须使用工具直接修改数据源。  
  
## <a name="see-also"></a>请参阅  
 [维度特性属性参考](dimension-attribute-properties-reference.md)   
 [父子维度中的自定义汇总运算符](parent-child-dimension-attributes-custom-rollup-operators.md)   
 [在维度设计器中启动商业智能向导](database-dimensions-bi-wizard-in-dimension-designer.md)  
  
  