---
title: 表达式（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 76d3ac86-650c-46fe-8086-8b3edcea3882
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 0ec516a74d28ff868e8a20d1c3d5cd568d3420ee
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53352795"
---
# <a name="expressions-report-builder-and-ssrs"></a>表达式（报表生成器和 SSRS）
  表达式在报表中被广泛使用，以便对数据进行检索、计算、显示、分组、排序、筛选、参数化和格式设置。 许多报表项属性都可以设置为表达式。 表达式可帮助您控制报表的内容、设计和交互。 表达式以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]编写，保存在报表定义中，并且在运行报表时由报表处理器计算。  
  
 与 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Office Excel 之类的应用程序（在此类应用程序中，直接在工作表中使用数据）不同，在报表中，您使用作为数据的占位符的表达式。 若要查看来自已计算表达式的实际数据，您必须预览报表。 在运行报表时，报表处理器在合并报表数据和报表布局元素（例如表和图表）时对每个表达式进行计算。  
  
 在您设计报表时，系统将为您设置针对报表项的许多表达式。 例如，将一个字段从数据窗格拖到报表设计图面上的表单元时，文本框值将设置为针对该字段的简单表达式。 在下图中，“报表数据”窗格显示数据集字段 ID、Name、SalesTerritory、Code 和 Sales。 三个字段已添加到该表中：[Name]、[Code] 和 [Sales]。 设计图面上的标志 [Name] 表示基础表达式 `=Fields!Name.Value`。  
  
 ![rs_DataDesignandPreview](../media/rs-datadesignandpreview.gif "rs_DataDesignandPreview")  
  
 在您预览报表时，报表处理器将表数据区域和来自数据连接的实际数据相结合，并且为结果集中的每一行在表中显示一行。  
  
 若要手动输入表达式，请在设计图面上选择某个项，然后使用快捷菜单和对话框设置该项的属性。 看到 ***(fx)*** 按钮或者在下拉列表中看到值 `<Expression>` 时，表明可以将该属性设置为表达式。 有关详细信息，请参阅[添加表达式（报表生成器和 SSRS）](add-an-expression-report-builder-and-ssrs.md)。  
  
 有关详细信息和示例，请参阅下列主题：  
  
-   [在报表中使用表达式（报表生成器和 SSRS）](expression-uses-in-reports-report-builder-and-ssrs.md)  
  
-   [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)  
  
-   [筛选器公式示例（报表生成器和 SSRS）](filter-equation-examples-report-builder-and-ssrs.md)  
  
-   [组表达式示例（报表生成器和 SSRS）](group-expression-examples-report-builder-and-ssrs.md)  
  
-   [教程&#40;报表生成器&#41;](../report-builder-tutorials.md)  
  
-   [Reporting Services 教程 (SSRS)](../reporting-services-tutorials-ssrs.md)  
  
-   [报表示例（报表生成器和 SSRS）](https://go.microsoft.com/fwlink/?LinkId=198283)  
  
 若要开发复杂表达式或使用自定义代码或自定义程序集的表达式，建议您使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中的报表设计器。 有关详细信息，请参阅 [报表设计器的表达式中的自定义代码和程序集引用 (SSRS)](custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Types"></a> 了解简单表达式和复杂表达式  
 表达式通常以等号 (=) 开头，以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]语言编写。 表达式可包含以下项的组合：常量、运算符、对内置值（字段、集合和函数）的引用以及对外部或自定义代码的引用。  
  
 您可以使用表达式来指定许多报表项属性的值。 最常见的属性是文本框和占位符文本的值。 通常，如果某一文本框只包含一个表达式，则该表达式是文本框属性的值。 如果某一文本框包含多个表达式，则每个表达式都是该文本框中占位符文本的值。  
  
 默认情况下，表达式作为“简单表达式”  或“复杂表达式” 出现在报表设计图面上。  
  
-   **简单** ：包含对内置集合中单个项（例如，数据集字段、参数或内置字段）的引用的简单表达式。 在设计图面上，简单表达式将出现在括号中。 例如， `[FieldName]` 将对应于基础表达式 `=Fields!FieldName.Value`。 当您创建报表布局并且将项从“报表数据”窗格拖到设计图面时，系统将自动为您创建简单表达式。 有关表示不同内置集合的符号的详细信息，请参阅 [了解简单表达式中的前缀符号](#DisplayText)。  
  
-   **复杂** ：复杂表达式包含对多个内置引用、运算符和函数调用的引用。 当表达式值包括多个简单引用时，复杂表达式将以 <\<Expr>> 形式出现。 若要查看表达式，请将鼠标指针悬停在表达式上并使用工具提示。 若要编辑表达式，请在 **“表达式”** 对话框中打开它。  
  
 下图显示针对文本框和占位符文本的典型的简单和复杂表达式。  
  
 ![rs_ExpressionDefaultFormat](../media/rs-expressiondefaultformat.gif "rs_ExpressionDefaultFormat")  
  
 若要显示简单值而非表达式文本，请将格式设置应用于文本框或占位符文本。 下图显示了切换为显示简单值的报表设计图面：  
  
 ![rs_ExpressionSampleValuesFormat](../media/rs-expressionsamplevaluesformat.gif "rs_ExpressionSampleValuesFormat")  
  
 有关详细信息，请参阅 [设置文本和占位符的格式（报表生成器和 SSRS）](formatting-text-and-placeholders-report-builder-and-ssrs.md)的详细信息。  
  

  
### <a name="report-model-formulas"></a>报表模型公式  
 为使用报表模型作为数据源的数据集设计查询时，可以创建“公式” 。 公式用于对报表中基于报表模型的数据的值进行计算。  
  
 有关详细信息，请参阅[报表模型查询中的公式（报表生成器和 SSRS）](formulas-in-report-model-queries-report-builder-and-ssrs.md)。  
  

  

  
##  <a name="DisplayText"></a> 了解简单表达式中的前缀符号  
 简单表达式使用符号来指示引用是指向字段、参数、内置集合还是指向 ReportItems 集合。 下表显示了显示文本和表达式文本的示例：  
  
|项|显示文本示例|表达式文本示例|  
|----------|--------------------------|-----------------------------|  
|数据集字段|`[Sales]`<br /><br /> `[SUM(Sales)]`<br /><br /> `[FIRST(Store)]`|`=Fields!Sales.Value`<br /><br /> `=Sum(Fields!Sales.Value)`<br /><br /> `=First(Fields!Store.Value)`|  
|报表参数|`[@Param]`<br /><br /> `[@Param.Label]`|`=Parameters!Param.Value`<br /><br /> `=Parameters!Param.Label`|  
|内置字段|`[&ReportName]`|`=Globals!ReportName.Value`|  
|用于显示文本的文字字符|`\[Sales\]`|`[Sales]`|  
  

  
##  <a name="References"></a> 编写复杂表达式  
 表达式可包括对函数、运算符、常量、字段、参数、内置集合中的项以及对嵌入的自定义代码或自定义程序集的引用。  
  
> [!NOTE]
>  若要开发复杂表达式或使用自定义代码或自定义程序集的表达式，建议您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中的报表设计器。 有关详细信息，请参阅 [报表设计器的表达式中的自定义代码和程序集引用 (SSRS)](custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)。  
  
 下表列出了可以包含在表达式中的引用类型：  
  
|References|Description|示例|  
|----------------|-----------------|-------------|  
|[常量](expressions-report-builder-and-ssrs.md)|介绍能以交互方式访问需要常量值的属性（例如字体颜色）的常量。|`="Blue"`|  
|[运算符](operators-in-expressions-report-builder-and-ssrs.md)|描述可用于合并表达式中的引用的运算符。 例如，`&` 运算符用于串联字符串。|`="The report ran at: " & Globals!ExecutionTime & "."`|  
|[内置集合](built-in-collections-in-expressions-report-builder.md)|介绍可在表达式中包含的内置集合，例如 `Fields`、 `Parameters`和 `Variables`。|`=Fields!Sales.Value`<br /><br /> `=Parameters!Store.Value`<br /><br /> `=Variables!MyCalculation.Value`|  
|[内置报表函数和聚合函数](report-builder-functions-aggregate-functions-reference.md)|介绍可从表达式中访问的内置函数，例如 `Sum` 或 `Previous`。|`=Previous(Sum(Fields!Sales.Value))`|  
|[报表设计器的表达式中的自定义代码和程序集引用 (SSRS)](custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)|介绍如何访问内置 CLR 类 <xref:System.Math> 和 <xref:System.Convert>、其他 CLR 类、 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 运行时库函数或外部程序集中的方法。<br /><br /> 介绍如何访问嵌入在报表中的自定义代码或已编译成自定义程序集并安装在报表客户端和报表服务器上的自定义代码。|`=Sum(Fields!Sales.Value)`<br /><br /> `=CDate(Fields!SalesDate.Value)`<br /><br /> `=DateAdd("d",3,Fields!BirthDate.Value)`<br /><br /> `=Code.ToUSD(Fields!StandardCost.Value)`|  
  

  
##  <a name="Valid"></a> 验证表达式  
 创建用于特定报表项属性的表达式时，可包含在表达式中的引用取决于该报表项属性可接受的值以及对属性进行求值的作用域。 例如：  
  
-   默认情况下，在对表达式进行求值时表达式 [Sum] 计算处于作用域中的数据的和。 对于表单元，该作用域依赖于行和列组成员资格。 有关详细信息，请参阅 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
-   对于 Font 属性的值，该值的计算结果必须为字体名称。  
  
-   在设计时验证表达式语法。 在您发布报表时进行表达式作用域验证。 对于依赖于实际数据的验证，只能在运行时检测到错误。 其中的某些表达式将生成 #Error 作为呈现的报表中的错误消息。 为了帮助确定此类型的错误问题，您必须使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中的报表设计器。 报表设计器提供一个“输出”窗口，该窗口提供有关这些错误的详细信息。  
  
 有关详细信息，请参阅 [表达式引用（报表生成器和 SSRS）](expression-reference-report-builder-and-ssrs.md)。  
  

  
##  <a name="Section"></a> 本节内容  
 [添加表达式（报表生成器和 SSRS）](add-an-expression-report-builder-and-ssrs.md)  
  
 [在报表中使用表达式（报表生成器和 SSRS）](expression-uses-in-reports-report-builder-and-ssrs.md)  
  
 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
 [表达式引用（报表生成器和 SSRS）](expression-reference-report-builder-and-ssrs.md)  
  

  
## <a name="see-also"></a>请参阅  
 [“表达式”对话框](../expression-dialog-box.md)   
 [“表达式”对话框（报表生成器）](../expression-dialog-box-report-builder.md)  
  
  
