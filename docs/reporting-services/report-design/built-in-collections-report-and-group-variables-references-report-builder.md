---
title: 报表和组变量集合引用（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
f1_keywords:
- "10404"
- "10083"
- sql13.rtp.rptdesigner.groupproperties.variables.f1
- sql13.rtp.rptdesigner.categorygroupproperties.variables.f1
- sql13.rtp.rptdesigner.reportproperties.variables.f1
- "10292"
- sql13.rtp.rptdesigner.seriesgroupproperties.variables.f1
- "10412"
ms.assetid: 4be5b463-3ce2-483d-a3c6-dae752cb543e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 91ff438183c197511ee33ee0f0baa779feb2b768
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43268075"
---
# <a name="built-in-collections---report-and-group-variables-references-report-builder"></a>内置集合 - 报表和组变量引用（报表生成器）
  在报表的表达式中需要多次使用某个复杂计算时，您可能需要创建一个变量。 您可以创建一个报表变量或组变量。 变量名称在报表中必须是唯一的。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-variables"></a>报表变量  
 使用报表变量可保存时间相关的计算的值（例如货币汇率或时间戳），或者保存多次引用的复杂计算的值。 默认情况下，报表变量计算一次即可在报表中的表达式中使用。 报表变量默认为只读。 您可以更改该默认设置以使报表变量成为读写的。 在再次处理该报表之前，报表变量中的值将保留在整个会话中。  
  
 若要添加报表变量，请打开“报表属性”对话框，单击“变量”，然后提供名称和值。 名称是区分大小写的字符串，以字母开头，不含空格。 名称可以包含字母、数字或下划线 (_)。  
  
 若要引用表达式中的变量，请使用全局集合语法，例如 `=Variables!CustomTimeStamp.Value`。 在设计图面上，文本框中的值显示为 `<<Expr>>`。  
  
 可以按下列方式使用报表变量：  
  
-   **只读使用** ：设置值一次以便为报表会话创建一个常量，例如创建一个时间戳。  
  
     因为当用户在报表中翻页时，文本框中的表达式将按需计算，所以，如果用户通过使用“上一页”按钮向前和向后翻页，动态值（例如，包括返回时间的 `Now()` 函数的表达式）可以返回不同的值。 通过将报表变量的值设置为表达式 `=Now()`，然后在表达式中添加变量，可确保整个报表处理过程中使用相同的值。  
  
-   **读写使用** ：设置值一次并在报表会话中序列化该值。 变量的读写选项提供了一个比在报表定义的代码块中使用静态变量更好的选择。  
  
     如果清除了某一变量的“只读”选项，则该变量的 Writable 属性将设置为“true”。 若要从某一表达式更新值，请使用 SetValue 方法，例如 `=Variables!MyVariable.SetValue("123")`。  
  
    > [!NOTE]  
    >  您不能控制报表处理器何时初始化一个变量或何时对更新变量的表达式进行计算。 变量初始化的执行顺序未定义。  
  
 有关会话的详细信息，请参阅 [Previewing Reports in Report Builder](../../reporting-services/report-builder/previewing-reports-in-report-builder.md)。  
  
## <a name="group-variables"></a>组变量  
 使用组变量可在组的作用域中计算一次复杂表达式。 组变量仅在组及其子组的作用域中有效。  
  
 例如，假定一个数据区域显示不同税收类别项目的库存数据，您希望对每种类别分别采用不同的税率。 可以对 Category 中的数据进行分组，并对父组定义一个 *Tax* 变量。 然后为每个税收类别的 *ItemTax* 定义一个组变量，再将每个不同的 Category 子组分配给正确的组变量。 例如：  
  
-   对于基于 `[Category]`的父组，使用 *值定义变量* Tax `[Tax]`。 假定类别值为 Food 和 Clothing。  
  
-   对于基于 `[Subcategory]`的子组，将变量 *ItemsTax* 定义为 `=Variables!Tax.Value * Sum(Fields!Price.Value)`。 假定 Food 类别中的子类别值为 Beverages 和 Bread。 假定 Clothing 类别中的子类别值为 Shirts 和 Hats。  
  
-   在子组行中的文本框添加表达式 `=Variables!ItemsTax.Value`。  
  
     文本框中显示按照 Food 税计算的 Beverages 和 Bread 以及按照 Clothing 税计算的 Shirts 和 Hats 的总税额。  
  
 若要添加组变量，打开 **“Tablix 组属性”** 对话框，单击 **“变量”**，然后输入一个名称和一个值。 组变量在每个唯一组值中计算一次。  
  
 若要引用表达式中的变量，请使用全局集合语法，例如 `=Variables!GroupDescription.Value`。 在设计图面上，文本框中的值显示为 `<<Expr>>`。  
  
## <a name="see-also"></a>另请参阅  
 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [表达式中的内置集合（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)   
 [表达式示例（报表生成器和 SSRS）](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
