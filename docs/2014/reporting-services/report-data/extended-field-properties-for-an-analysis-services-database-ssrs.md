---
title: Analysis Services 数据库的扩展字段属性 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1d7d87e2-bf0d-4ebb-a287-80b5a967a3f2
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 5912a29ddfd19ef5e191be6c4d102117d125421d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137692"
---
# <a name="extended-field-properties-for-an-analysis-services-database-ssrs"></a>Analysis Services 数据库的扩展字段属性 (SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据处理扩展插件支持扩展字段属性。 扩展字段属性是除字段属性 `Value` 和 `IsMissing` 之外的属性，可用于数据源并受数据处理扩展插件支持。 扩展属性并不作为报表数据集的字段集合的一部分显示在“报表数据”窗格中。 你可以在报表中包含扩展的字段属性值，通过编写通过使用内置的名称来指定这些表达式`Fields`集合。  
  
 扩展属性包括预定义属性和自定义属性。 预定义的属性是普遍适用于多个数据源映射到特定的字段属性名称，并且可以访问通过内置的属性`Fields`按名称的集合。 自定义属性是特定于每个数据访问接口的属性，只能通过内置 `Fields` 集合，使用将扩展属性名称用作字符串的语法进行访问。  
  
 在图形模式下使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] MDX 查询设计器定义查询时，一组预定义的单元属性和维度属性会自动添加到 MDX 查询。 您只能使用在您的报表的 MDX 查询中专门列出的扩展属性。 根据您的报表，可能需要修改默认 MDX 命令文本才能包含多维数据集中定义的其他维度或自定义属性。 有关 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据源中的可用扩展字段的详细信息，请参阅[创建和使用属性值 (MDX)](../../analysis-services/creating-and-using-property-values-mdx.md)。  
  
## <a name="working-with-field-properties-in-a-report"></a>在报表中使用字段属性  
 扩展字段属性包括预定义属性和数据访问接口特定属性。 即使字段属性位于为数据集生成的查询中，它们也不会与字段列表一起显示在 **“报表数据”** 窗格中，因此，不能将字段属性拖至报表设计图面中。 相反，您必须将该字段拖动到报表，然后更改`Value`到你想要使用的属性的字段的属性。 例如，如果已设置多维数据集的单元格数据的格式，则可以通过表达式 `=Fields!FieldName.FormattedValue`，来使用 FormattedValue 字段属性。  
  
 若要引用未预定义的扩展属性，请在表达式中使用以下语法：  
  
-   *Fields!FieldName("PropertyName")*  
  
## <a name="predefined-field-properties"></a>预定义的字段属性  
 在大多数情况下，预定义的字段属性应用于度量值、级别或维度。 预定义的字段属性必须在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据源中存储相应的值。 如果值不存在，或者（例如）对某个级别指定了仅适用于度量值的字段属性，则该属性将返回空值。  
  
 可以使用以下任一语法引用表达式中的预定义属性：  
  
-   *Fields!FieldName.PropertyName*  
  
-   *Fields!FieldName("PropertyName")*  
  
 下表提供了您可以使用的预定义字段属性的列表：  
  
|**属性**|**类型**|**说明或所需的值**|  
|------------------|--------------|---------------------------------------|  
|`Value`|`Object`|指定字段的数据值。|  
|`IsMissing`|`Boolean`|指示是否在结果数据集中找到了该字段。|  
|`UniqueName`|`String`|返回级别的完全限定名称。 例如，`UniqueName`员工可能的值 *[员工]。 [员工部门]。[部门]。 （&) [销售]。 （& a) [北美销售经理]。 （&) [272]*。|  
|`BackgroundColor`|`String`|返回数据库中为该字段定义的背景颜色。|  
|`Color`|`String`|返回数据库中为该项定义的前景色。|  
|`FontFamily`|`String`|返回数据库中为该项定义的字体的名称。|  
|`FontSize`|`String`|返回数据库中为该项定义的字体的字号。|  
|`FontWeight`|`String`|返回数据库中为该项定义的字体的粗细。|  
|`FontStyle`|`String`|返回数据库中为该项定义的字体的样式。|  
|`TextDecoration`|`String`|返回数据库中为该项定义的特殊文本格式设置。|  
|`FormattedValue`|`String`|返回度量值或关键数字的格式值。 例如，`FormattedValue`属性**销售额配额**返回货币格式，如 $1,124,400.00。|  
|`Key`|`Object`|返回级别的键。|  
|`LevelNumber`|`Integer`|针对父子层次结构返回级别号或维度编号。|  
|`ParentUniqueName`|`String`|针对父子层次结构返回父级的完全限定名称。|  
  
> [!NOTE]  
>  仅当数据源（如 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多维数据集）在运行报表并检索报表数据集的数据时，为这些扩展字段属性提供值，这些值才存在。 然后，您可以使用下面介绍的语法从任意表达式引用这些字段属性值。 但是，由于这些字段专用于此数据访问接口，因此，对这些值所做的更改不会随报表定义一同保存。  
  
### <a name="example-extended-properties"></a>扩展属性示例  
 为了说明扩展属性，以下 MDX 查询和结果集包含了为多维数据集定义的某维度属性的多个可用成员属性。 包含的成员属性为 MEMBER_CAPTION、UNIQUENAME、Properties("Day Name")、MEMBER_VALUE、PARENT_UNIQUE_NAME 和 MEMBER_KEY。  
  
 此 MDX 查询针对 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] DW 数据库（随 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 示例数据库提供）中的 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 多维数据集运行。  
  
```  
WITH MEMBER [Measures].[DateCaption]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_CAPTION'   
   MEMBER [Measures].[DateUniqueName]   
      AS '[Date].[Date].CURRENTMEMBER.UNIQUENAME'   
   MEMBER [Measures].[DateDayName]   
      AS '[Date].[Date].Properties("Day Name")'   
   MEMBER [Measures].[DateValueinOriginalDatatype]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_VALUE'   
   MEMBER [Measures].[DateParentUniqueName]   
      AS '[Date].[Date].CURRENTMEMBER.PARENT_UNIQUE_NAME'   
   MEMBER [Measures].[DateMemberKeyinOriginalDatatype]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_KEY'   
SELECT {  
   [Measures].[DateCaption],   
   [Measures].[DateUniqueName],   
   [Measures].[DateDayName],   
   [Measures].[DateValueinOriginalDatatype],  
   [Measures].[DateParentUniqueName],  
   [Measures].[DateMemberKeyinOriginalDatatype]  
   } ON COLUMNS , [Date].[Date].ALLMEMBERS ON ROWS   
FROM [Adventure Works]  
  
```  
  
 在 MDX 查询窗格中运行此查询时，您将获得一个包含 1158 行的结果集。 下表显示了其中的前四行。  
  
|DateCaption|DateUniqueName|DateDayName|DateValueinOriginalDatatype|DateParentUniqueName|DateMemberKeyinOriginalDatatype|  
|-----------------|--------------------|-----------------|---------------------------------|--------------------------|-------------------------------------|  
|All Periods|[Date].[Date].[All Periods]|(null)|(null)|(null)|0|  
|1-Jul-01|[Date].[Date].&[1]|星期日|7/1/2001|[Date].[Date].[All Periods]|@shouldalert|  
|2-Jul-01|[Date].[Date].&[2]|星期一|7/2/2001|[Date].[Date].[All Periods]|2|  
|3-Jul-01|[Date].[Date].&[3]|星期二|7/3/2001|[Date].[Date].[All Periods]|3|  
  
 对于使用图形模式下的默认 MDX 查询设计器生成的 MDX 查询，其维度属性只包括 MEMBER_CAPTION 和 UNIQUENAME。 默认情况下，这些值始终为 `String` 数据类型。  
  
 如果需要成员属性采用其原始数据类型，则可通过在基于文本的查询设计器中修改默认 MDX 语句，来包含附加属性 MEMBER_VALUE。 在下面的简单 MDX 语句中，MEMBER_VALUE 已添加到要检索的维度属性列表中。  
  
```  
SELECT NON EMPTY {[Measures].[Order Count]} ON COLUMNS,   
NON EMPTY { ([Date].[Month of Year].[Month of Year] ) }   
DIMENSION PROPERTIES   
   MEMBER_CAPTION, MEMBER_UNIQUE_NAME, MEMBER_VALUE ON ROWS   
FROM [Adventure Works]  
CELL PROPERTIES   
   VALUE, BACK_COLOR, FORE_COLOR,   
   FORMATTED_VALUE, FORMAT_STRING,   
   FONT_NAME, FONT_SIZE, FONT_FLAGS  
```  
  
 下表显示了 MDX“结果”窗格中的前四行结果。  
  
|Month of Year|Order Count|  
|-------------------|-----------------|  
|January|2,481|  
|February|2,684|  
|March|2,749|  
|April|2,739|  
  
 即使属性是 MDX 选择语句的一部分，它们也不会显示在结果集列中。 尽管如此，使用扩展属性功能仍可将这些数据用于报表。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]的 MDX 查询结果窗格中，你可以双击单元格并查看单元格的属性值（如果在多维数据集中进行了设置）。 如果双击第一个包含 1,379 的 Order Count 单元，则会看到一个包含以下单元属性的弹出窗口：  
  
|“属性”|Value|  
|--------------|-----------|  
|CellOrdinal|0|  
|Value|2481|  
|BACK_COLOR|(null)|  
|FORE_COLOR|(null)|  
|FORMATTED_VALUE|2,481|  
|FORMAT_STRING|#,#|  
|FONT_NAME|(null)|  
|FONT_SIZE|(null)|  
|FONT_FLAGS|(null)|  
  
 如果使用此查询创建报表数据集，并将该数据集绑定到一个表，则可以看到字段的默认 VALUE 属性，例如 `=Fields!Month_of_Year!Value`。 如果将此表达式设置表的排序表达式，则结果将为表进行排序，按字母顺序按月因为值字段使用`String`数据类型。 若要按月份在一年中的顺序（即一月排在第一位，十二月排在最后）对该表进行排序，请使用以下表达式：  
  
```  
=Fields!Month_of_Year("MEMBER_VALUE")  
```  
  
 这将使用数据源中字段的原始整数数据类型对其值进行排序。  
  
## <a name="see-also"></a>请参阅  
 [表达式（报表生成器和 SSRS）](../report-design/expressions-report-builder-and-ssrs.md)   
 [在表达式中的内置集合&#40;报表生成器和 SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md)   
 [数据集字段集合（报表生成器和 SSRS）](dataset-fields-collection-report-builder-and-ssrs.md)  
  
  