---
title: 有条件拆分转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.conditionalsplittrans.f1
helpviewer_keywords:
- Conditional Split transformation
- route rows to different outputs [Integration Services]
ms.assetid: 3f8b5825-226f-413c-ba8f-0bb931ca3770
author: chugugrace
ms.author: chugu
ms.openlocfilehash: eba0f7b305d3b08692c69cc44202f9d565ca9d38
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85430934"
---
# <a name="conditional-split-transformation"></a>有条件拆分转换
  有条件拆分转换可以根据数据内容将数据行路由到不同的输出。 有条件拆分转换的实现类似于编程语言中的 CASE 决策结构。 此转换将计算表达式，并且根据结果将数据行定向到指定输出。 此转换还提供默认输出，因此，如果某行与任何表达式都不匹配，它会被定向到默认输出。  
  
## <a name="configuration-of-the-conditional-split-transformation"></a>有条件拆分转换的配置  
 可以按照下列方式配置有条件拆分转换：  
  
-   提供一个表达式，此表达式将转换要测试的每个条件都计算为一个布尔值。  
  
-   指定计算条件的顺序。 顺序很重要，因为行将被发送到对应于第一个计算结果为 true 的条件的输出。  
  
-   指定转换的默认输出。 此转换要求指定默认输出。  
  
 每个输入行只能被发送到一个输出，即第一个计算结果为 true 的条件的输出。 例如，下列条件将 **FirstName** 列中以字母 *A* 开头的所有行定向到一个输出，将以字母 *B* 开头的行定向到另一个输出，将所有其他行定向到默认输出。  
  
 输出 1  
  
 `SUBSTRING(FirstName,1,1) == "A"`  
  
 输出 2  
  
 `SUBSTRING(FirstName,1,1) == "B"`  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包含的函数和运算符可用于创建计算输入数据并定向输出数据的表达式。 有关详细信息，请参阅 [Integration Services (SSIS) 表达式](../../expressions/integration-services-ssis-expressions.md)。  
  
 有条件拆分转换包括 `FriendlyExpression` 自定义属性。 加载包时，可以通过属性表达式更新此属性。 有关详细信息，请参阅 [在包中使用属性表达式](../../expressions/use-property-expressions-in-packages.md) 和 [转换自定义属性](transformation-custom-properties.md)。  
  
 此转换具有一个输入、一个或多个输出和一个错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 **“有条件拆分转换编辑器”** 对话框中设置的属性的详细信息，请参阅 [Conditional Split Transformation Editor](../../conditional-split-transformation-editor.md)。  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](../../common-properties.md)  
  
-   [Transformation Custom Properties](transformation-custom-properties.md)  
  
 有关如何设置属性的详细信息，请单击下列主题之一：  
  
-   [使用有条件拆分转换拆分数据集](conditional-split-transformation.md)  
  
-   [设置数据流组件的属性](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [使用有条件拆分转换拆分数据集](conditional-split-transformation.md)  
  
## <a name="see-also"></a>另请参阅  
 [数据流](../data-flow.md)   
 [Integration Services 转换](integration-services-transformations.md)  
  
  
