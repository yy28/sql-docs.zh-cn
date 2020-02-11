---
title: 数据集字段集合引用（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 006c6bd3-d776-4c20-9092-32e40688ac49
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 659fade9e10edc32c2444bf024fd475ea78a5d1d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66106453"
---
# <a name="dataset-fields-collection-references-report-builder-and-ssrs"></a>数据集字段集合引用（报表生成器和 SSRS）
  报表中的每个数据集都包含一个字段集合。 字段集合由数据集查询指定的字段集以及你创建的任何其他计算字段组成。 创建数据集后，字段集合将显示在 **“报表数据”** 窗格中。  
  
 表达式中的简单字段引用在设计图面上显示为简单表达式。 例如，将字段 `Sales` 从“报表数据”窗格拖到设计图面上的表单元时，将显示 `[Sales]` 。 这表示对文本框 Value 属性设置的是基础表达式 `=Fields!Sales.Value` 。 运行报表时，报表处理器会计算此表达式，并在表单元的文本框中显示数据源中的实际数据。 有关详细信息，请参阅[表达式（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)和[数据集字段集合（报表生成器和 SSRS）](../report-data/dataset-fields-collection-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="displaying-the-field-collection-for-a-dataset"></a>显示数据集的字段集合  
 若要显示字段集合的各个值，可将每个字段拖到表详细信息行，并运行报表。 表详细信息行或列表数据区域中的引用将显示数据集中每一行的值。  
  
 若要显示字段的汇总值，可将每个数值字段都拖到矩阵的数据区域中。 总计行的默认聚合函数为 Sum，例如， `=Sum(Fields!Sales.Value)`。 可以更改默认函数以便计算不同的总计。 有关详细信息，请参阅 [聚合函数引用（报表生成器和 SSRS）](report-builder-functions-aggregate-functions-reference.md)。  
  
 若要在设计图面（而非数据区域的一部分）的文本框中直接显示字段集合的汇总值，必须指定数据集名称作为聚合函数的作用域。 例如，对于名为 `SalesData`的数据集，以下表达式指定了字段 `Sales`所有值的总计： `=Sum(Fields!Sales,"SalesData")`。  
  
 使用“表达式”对话框定义简单字段引用时，可以在“类别”窗格中选择字段集合，并查看“字段”窗格中的可用字段列表********。 每个字段都具有多个属性，包括 Value 和 IsMissing。 其余属性是数据集可能可用的预定义扩展字段属性，具体取决于数据源类型。  
  
### <a name="detecting-nulls-for-a-dataset-field"></a>检测数据集字段的 Null 值  
 若要检测为 Null（在 `Nothing` 中为 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]）的字段值，可使用函数 `IsNothing`。 当以下表达式放置在表详细信息行的文本框中时，将测试字段 `MiddleName` 。如果值为 Null，则显示文本“No Middle Name”，如果值不为 Null，则使用该字段值本身：  
  
 `=IIF(IsNothing(Fields!MiddleName.Value),"No Middle Name",Fields!MiddleName.Value)`  
  
### <a name="detecting-missing-fields-for-dynamic-queries-at-run-time"></a>在运行时检测动态字段的缺失字段  
 默认情况下，字段集合中的项有两个属性：Value 和 IsMissing。 IsMissing 属性指示设计时为数据集定义的字段是否包含在运行时检索到的字段中。 例如，查询可能调用一个结果集随输入参数变化的存储过程，或者查询可能为 `SELECT * FROM` *\<table>，其中表定义会发生变化*。  
  
> [!NOTE]  
>  IsMissing 可针对任何类型的数据源检测在设计时和运行时数据集架构中的更改。 IsMissing 不能用于检测多维数据集中的空成员，并且与`EMPTY`和`NON EMPTY`的 MDX 查询语言概念无关。  
  
 可以使用自定义代码测试 IsMissing 属性以确定某个字段是否存在于结果集中。 不能使用包含 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 函数调用（如 `IIF` 或 `SWITCH`）的表达式测试字段是否存在，因为 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 会计算函数调用中的所有参数，这将导致计算对缺失字段的引用时出错。  
  
#### <a name="example-for-controlling-the-visibility-of-a-dynamic-column-for-a-missing-field"></a>控制缺失字段动态列的可见性的示例  
 若要设置一个表达式，用于控制显示数据集中某个字段的列的可见性，必须首先定义一个自定义代码函数，该函数根据该字段是否缺失返回一个布尔值。 例如，如果该字段缺失，则以下自定义代码函数将返回 True；如果该字段存在，则返回 False。  
  
```  
Public Function IsFieldMissing(field as Field) as Boolean  
 If (field.IsMissing) Then  
 Return True  
  Else   
  Return False  
 End If  
End Function  
```  
  
 若要将此函数用于控制列的可见性，请将列的 Hidden 属性设置为以下表达式：  
  
 `=Code.IsFieldMissing(Fields!FieldName)`  
  
 当字段不存在时将隐藏该列。  
  
#### <a name="example-for-controlling-the-text-box-value-for-a-missing-field"></a>控制缺失字段的文本框值的示例  
 若要使用您编写的文本来代替缺失字段的值，必须编写自定义代码，以便在字段缺失时返回可用于代替字段值的文本。 例如，如果该字段存在，则以下自定义代码函数将返回该字段的值，如果该字段不存在，则返回指定为第二个参数的消息：  
  
```  
Public Function IsFieldMissingThenString(field as Field, strMessage as String) as String  
 If (field.IsMissing) Then  
  Return strMessage  
 Else   
  Return field.Value  
  End If  
End Function  
```  
  
 若要在文本框中使用此函数，请将以下表达式添加到 Value 属性：  
  
 `=Code.IsFieldMissingThenString(Fields!FieldName,"Missing")`  
  
 文本框显示字段值或您指定的文本。  
  
### <a name="using-extended-field-properties"></a>使用扩展字段属性  
 扩展字段属性是由数据处理扩展插件为字段定义的其他属性，这些属性由数据集的数据源类型确定。 扩展字段属性可以是预定义的，也可以特定于某个数据源类型。 有关详细信息，请参阅 [Analysis Services 数据库的扩展字段属性 (SSRS)](../report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md)。  
  
 如果指定了该字段不支持的属性，则表达式的计算结果为 `null`（在 `Nothing` 中为 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]）。 如果数据访问接口不支持扩展字段属性，或在执行查询时找不到该字段，则对于 `null` 和 `Nothing` 类型的属性，属性值为 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]（在 `String` 中为 `Object`）；对于 `Integer` 类型的属性，属性值为零 (0)。 数据处理扩展插件可以通过优化包括此语法的查询来充分利用预定义属性。  
  
## <a name="see-also"></a>另请参阅  
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [将数据添加到报表 &#40;报表生成器和 SSRS&#41;](../report-data/report-datasets-ssrs.md)  
  
  
