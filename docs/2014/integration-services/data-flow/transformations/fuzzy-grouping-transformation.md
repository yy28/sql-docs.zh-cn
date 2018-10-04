---
title: 模糊分组转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtrans.f1
helpviewer_keywords:
- cleaning data
- comparing data
- token delimiters [Integration Services]
- temporary indexes [Integration Services]
- Fuzzy Grouping transformation
- temporary tables [Integration Services]
- grouping data
- standardizing data [Integration Services]
- columns [Integration Services], standardizing
- similarity thresholds [Integration Services]
- data cleaning [Integration Services]
- duplicate data [Integration Services]
ms.assetid: e43f17bd-9d13-4a8f-9f29-cce44cac1025
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8f0b1fc213fb1916421b1c9b0f02bb82b5553770
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48122998"
---
# <a name="fuzzy-grouping-transformation"></a>模糊分组转换
  模糊分组转换执行数据清理任务，它首先查找可能重复的数据行，然后选择要在对数据进行标准化的过程中使用的规范数据行。  
  
> [!NOTE]  
>  有关模糊分组转换（包括性能和内存限制）的详细信息，请参阅白皮书 [SQL Server Integration Services 2005 中的模糊查找和模糊分组](http://go.microsoft.com/fwlink/?LinkId=96604)。  
  
 模糊分组转换要求与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的实例建立连接，以创建该转换算法完成工作所需的临时 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 表。 该连接必须解析为有权在数据库中创建表的用户。  
  
 若要配置该转换，您必须选择要在确定重复项时使用的输入列，而且必须为每列选择匹配类型（模糊匹配或完全匹配）。 完全匹配保证只对该列中具有相同值的行进行分组。 完全匹配可以应用到除 DT_TEXT、DT_NTEXT 和 DT_IMAGE 之外的任何 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 数据类型的列。 模糊匹配对具有相似值的行进行分组。 近似匹配数据的方法基于用户指定的相似性得分。 在模糊匹配中，只能使用具有 DT_WSTR 和 DT_STR 数据类型的列。 有关详细信息，请参阅 [Integration Services 数据类型](../integration-services-data-types.md)。  
  
 该转换输出包括所有输入列、一个或多个具有标准化数据的列以及一个包含相似性得分的列。 该得分是一个介于 0 和 1 之间的小数值。 规范行的得分为 1。 模糊组中其他行具有的得分指明该行与规范行的匹配程度。 得分越接近 1，行与规范行的匹配程度越高。 如果模糊组包括与规范行完全匹配的行，则这些行的得分也为 1。 该转换不删除这些重复的行；它通过创建一个将规范行与相似行关联的键对重复行进行分组。  
  
 该转换为每个输入行产生一个输出行，同时还包括下面的附加列：  
  
-   **_key_in**，唯一标识每行的列。  
  
-   **_key_out**，标识一组重复行的列。 在规范数据行中， **_key_out** 列的值就是 **_key_in** 列。 **_key_out** 中的值相同的行属于同一个组。 组的 **_key_out**值对应于规范数据行中 **_key_in** 值。  
  
-   **_score**，一个介于 0 和 1 之间的值，指示输入行与规范行之间的相似性。  
  
 这些都是默认列名，您可以将模糊分组转换配置为使用其他名称。 输出还提供了参与模糊分组的每列的相似性得分。  
  
 模糊分组转换包括两个用于自定义所执行的分组的功能：标记分隔符和相似性阈值。 该转换提供了一组用于对数据进行词汇切分的默认分隔符，但您可以添加新的分隔符以改善您数据的词汇切分。  
  
 相似性阈值指示该转换标识重复项的严格程度。 相似性阈值可以在组件级和列级设置。 列级相似性阈值只适用于执行模糊匹配的列。 相似性范围是 0 到 1。 阈值越接近 1，则行和列必须越相似，才能被认定为重复。 通过在组件级和列级别设置 MinSimilarity 属性，可以指定行和列之间的相似性阈值。 为了满足在组件级指定的相似性，所有列的所有行都必须具有大于或等于在组件级所指定的相似性阈值的相似性。  
  
 模糊分组转换计算相似性的内部度量值，如果行的相似性低于 MinSimilarity 中指定的值，则不对这些行进行分组。  
  
 若要确定适合您数据的相似性阈值，您可能需要使用不同的最低相似性阈值多次应用模糊分组转换。 在运行时，转换输出中的得分列包含组中每行的相似性得分。 您可以使用这些值来确定适合您数据的相似性阈值。 如果要增加相似性，应该将 MinSimilarity 设置为一个大于得分列中所示值的值。  
  
 您可以通过设置模糊分组转换输入中的列属性来自定义该转换所执行的分组。 例如，FuzzyComparisonFlags 属性指定该转换如何比较列中的字符串数据，ExactFuzzy 属性指定该转换是执行模糊匹配还是执行完全匹配。  
  
 可以通过设置 MaxMemoryUsage 自定义属性来配置模糊分组转换所使用的内存数量。 可以指定 MB 数，或使用值 0 以允许转换基于其需要和可用物理内存而使用动态内存数量。 加载包时，可以通过属性表达式来更新 MaxMemoryUsage 自定义属性。 有关详细信息，请参阅 [Integration Services (SSIS) 表达式](../../expressions/integration-services-ssis-expressions.md)、[在包中使用属性表达式](../../expressions/use-property-expressions-in-packages.md)和[转换自定义属性](transformation-custom-properties.md)。  
  
 此转换有一个输入和一个输出。 它不支持错误输出。  
  
## <a name="row-comparison"></a>行比较  
 在配置模糊分组转换时，可以指定该转换比较转换输入中的行所用的算法。 如果将 Exhaustive 属性设置为`true`，转换将输入中的所有其他行的输入中的每一行进行比较。 这种比较算法可以生成更准确的结果，但是除非输入中的行数很少，否则很有可能使转换的执行速度变得很慢。 若要避免性能问题，是建议将 Exhaustive 属性设置为`true`仅在包开发过程。  
  
## <a name="temporary-tables-and-indexes"></a>临时表和索引  
 在运行时，模糊分组转换会在该转换所连接到的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库中创建临时对象，例如表和索引，这些表和索引可能会非常大。 表和索引的大小与转换输入中的行数和模糊分组转换所创建的标记数成比例。  
  
 该转换也会查询这些临时表。 因此，应该考虑将模糊分组转换连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的非生产实例中，在生产服务器只有有限的可用磁盘空间时，尤其应该如此。  
  
 如果此转换所使用的表和索引位于本地计算机，则此转换的性能可能会提高。  
  
## <a name="configuration-of-the-fuzzy-grouping-transformation"></a>配置模糊分组转换  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 **“模糊分组转换编辑器”** 对话框中设置的属性的详细信息，请单击下列主题之一：  
  
-   [模糊分组转换编辑器&#40;连接管理器选项卡&#41;](../../fuzzy-grouping-transformation-editor-connection-manager-tab.md)  
  
-   [模糊分组转换编辑器&#40;列选项卡&#41;](../../fuzzy-grouping-transformation-editor-columns-tab.md)  
  
-   [模糊分组转换编辑器&#40;高级选项卡&#41;](../../fuzzy-grouping-transformation-editor-advanced-tab.md)  
  
 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](../../common-properties.md)  
  
-   [转换自定义属性](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何设置此任务的属性的详细信息，请单击下列主题之一：  
  
-   [使用模糊分组转换标识相似数据行](fuzzy-grouping-transformation.md)  
  
-   [设置数据流组件的属性](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="see-also"></a>请参阅  
 [模糊查找转换](lookup-transformation.md)   
 [Integration Services 转换](integration-services-transformations.md)  
  
  
