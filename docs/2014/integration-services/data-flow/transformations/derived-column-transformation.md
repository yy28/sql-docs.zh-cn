---
title: 派生列转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.derivedcolumntrans.f1
helpviewer_keywords:
- multiple derived columns
- expressions [Integration Services], derived columns
- derived columns
- columns [Integration Services], derivations
- Derived Column transformation
ms.assetid: 8eba755e-8e48-4233-bd1e-09a46bf2692f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2a2767de67eac1a0346f059e1a2c81a5698607dc
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59240992"
---
# <a name="derived-column-transformation"></a>派生列转换
  派生列转换通过对转换输入列应用表达式来创建新列值。 表达式可以包含来自转换输入的变量、函数、运算符和列的任意组合。 结果可作为新列添加，也可作为替换值插入到现有列。 派生列转换可定义多个派生列，任何变量或输入列都可以出现在多个表达式中。  
  
 可以使用此转换执行下列任务：  
  
-   将不同列的数据连接到一个派生列中。 例如，可以使用表达式 **将** FirstName **和** LastName **列中的值组合到名为**FullName `FirstName + " " + LastName`的单个派生列中。  
  
-   通过使用 SUBSTRING 之类的函数从字符串数据中提取字符，然后将结果存储到派生列中。 例如，可以使用表达式 **从** FirstName `SUBSTRING(FirstName,1,1)`列提取人名的首字母。  
  
-   对数值数据应用数学函数，然后将结果存储到派生列中。 例如，可以使用表达式 **将数值列**SalesTax `ROUND(SalesTax, 2)`的值更改为精确到小数点后两位。  
  
-   创建比较输入列和变量的表达式。 例如，可以使用表达式 **来比较变量** Version **与**ProductVersion **列中的数据，然后根据比较结果决定选用** Version **还是**ProductVersion `ProductVersion == @Version? ProductVersion : @Version`的值。  
  
-   提取日期时间值的某部分。 例如，可以通过表达式 `DATEPART("year",GETDATE())`使用 GETDATE 和 DATEPART 函数提取当前年份。  
  
-   使用表达式将日期字符串转换为特定格式。  
  
## <a name="configuration-of-the-derived-column-transformation"></a>派生列转换的配置  
 可以按照下列方式配置派生列转换：  
  
-   为每个输入列或即将更改的新列提供表达式。 有关详细信息，请参阅 [Integration Services (SSIS) 表达式](../../expressions/integration-services-ssis-expressions.md)。  
  
    > [!NOTE]  
    >  如果表达式引用了由派生列转换覆盖的输入列，则表达式使用列的原始值，而不是派生值。  
  
-   如果向新列中添加结果并且数据类型为 `string`，则需指定代码页。 有关详细信息，请参阅 [Comparing String Data](../comparing-string-data.md)。  
  
 派生列转换包括 FriendlyExpression 自定义属性。 加载包时，可以通过属性表达式更新此属性。 有关详细信息，请参阅 [在包中使用属性表达式](../../expressions/use-property-expressions-in-packages.md)和 [转换自定义属性](transformation-custom-properties.md)。  
  
 此转换有一个输入、一个常规输出和一个错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 **“派生列转换编辑器”** 对话框中设置的属性的详细信息，请参阅 [Derived Column Transformation Editor](../../derived-column-transformation-editor.md)。  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](../../common-properties.md)  
  
-   [Transformation Custom Properties](transformation-custom-properties.md)  
  
 有关如何设置属性的详细信息，请单击下列主题之一：  
  
-   [设置数据流组件的属性](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [使用派生列转换派生列值](derived-column-transformation.md)  
  
## <a name="related-content"></a>相关内容  
 social.technet.microsoft.com 上的技术文章 [SSIS 表达式示例](https://go.microsoft.com/fwlink/?LinkId=220761)  
  
 博客[如何使用 SSIS 拆分列数据](https://microsoft-ssis.blogspot.com/2012/10/split-multi-value-column-into-multiple.html)。  
  
  
