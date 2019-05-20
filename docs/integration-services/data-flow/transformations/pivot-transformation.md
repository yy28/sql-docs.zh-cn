---
title: 透视转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.pivottrans.f1
helpviewer_keywords:
- Pivot transformation
- normalized data [Integration Services]
- PivotUsage property
- datasets [Integration Services], normalized data
- less normalized data set [Integration Services]
ms.assetid: 55f5db6e-6777-435f-8a06-b68c129f8437
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8bc233f7b23d08b9fd697eeddfae683420be33c5
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726018"
---
# <a name="pivot-transformation"></a>透视转换

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  通过透视列值的输入数据，透视转换将规范的数据集转变成规范程度稍低、但更为简洁的版本。 例如，在列有客户名称、产品和购买数量的规范的 **Orders** 数据集中，任何购买多种产品的客户都有多行，每一行显示一种产品的详细订购信息。 此时，如果对产品列透视数据集，透视转换可以输出每个客户只有一行的数据集。 这一行列出该客户购买的所有产品，产品名称显示为列名，而数量则显示为产品列的值。 并非每个客户都购买所有产品，所以很多列可能包含空值。  
  
 透视数据集时，输入列在透视过程中扮演不同的角色。 列可以按以下方式参与：  
  
-   将列原封不动地传递到输出。 因为有许多输入行只能产生一个输出行，所以转换只复制列的第一个输入值。  
  
-   列作为一组记录的标识键或标识键的一部分。  
  
-   列定义透视。 此列中的值与已透视数据集中的列相关联。  
  
-   列包含置于透视所创建的列中的值。  
  
 此转换有一个输入、一个常规输出和一个错误输出。  
  
## <a name="sort-and-duplicate-rows"></a>排序和复制行  
 若要高效地透视数据，即在输出数据集中创建尽可能少的记录，就必须对透视列的输入数据进行排序。 如果数据未经排序，那么透视转换就可能为设置键（即定义集成员关系的列）中的每个值生成多个记录。 例如，如果对 **名称** 列透视数据集，但是没有对名称排序，则每个客户在输出数据集中可能有多行，因为 **名称** 中的值每次更改都会发生透视。  
  
 输入数据可能包含重复行，这会导致透视转换失败。 “重复行”表示在设置键列和透视列中具有相同值的行。 为了避免失败，可以将转换配置为将错误行重定向到错误输出或预先聚合值，以确保不存在重复行。  
  
##  <a name="options"></a> “透视”对话框中的选项  
 可以通过设置 **“透视”** 对话框中的选项来配置透视操作。 若要打开“透视”对话框，请在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中将透视转换添加到包，右键单击该组件，然后单击“编辑”。  
  
 以下列表介绍了 **“透视”** 对话框中的选项。  
  
 **透视键**  
 指定要用于跨表的最上面一行（标题行）的值的列。  
  
 **设置键**  
 指定要用于表左侧列的值的列。 必须在此列对输入日期排序。  
  
 **透视值**  
 指定要用于以下表值的列：它们不是标题行和左侧列中的值。  
  
 **忽略不匹配的透视键值并在 DataFlow 执行后报告这些值**  
 选择此选项，以将透视转换配置为在运行包时忽略包含“透视键”列中无法识别的值的行并将所有透视键值输出到日志消息。  
  
 还可以通过将 **PassThroughUnmatchedPivotKeys** 自定义属性设置为 **True**来将该转换配置为输出这些值。  
  
 **根据值生成透视输出列**  
 在此框中输入透视键值，以启用透视转换来创建每个值的输出列。 您可以在运行包之前输入值，或执行以下操作：  
  
1.  在“透视”对话框中选择“忽略不匹配的透视键值并在 DataFlow 执行后报告这些值”选项，然后单击“确定”以保存对透视转换的更改。  
  
2.  运行包。  
  
3.  包成功运行时，单击 **“进度”** 选项卡，从包含透视键值的透视转换中查找信息日志消息。  
  
4.  右键单击该消息，然后单击“复制消息正文”。  
  
5.  在 **“调试”** 菜单上单击 **“停止调试”** 以切换回设计模式。  
  
6.  右键单击该透视转换，然后单击“编辑”。  
  
7.  取消选中“忽略不匹配的透视键值并在 DataFlow 执行后报告这些值”选项，然后使用以下格式在“根据值生成透视输出列”框中粘贴透视键值：  
  
     [value1],[value2],[value3]  
  
 **立即生成列**  
 单击以便为在“根据值生成透视输出列”框中列出的每个透视键值创建输出列。  
  
 输出列显示在 **“现有的透视输出列”** 框中。  
  
 **“现有的透视输出列”**  
 列出透视键值的输出列。  
  
 下表显示对 **年** 列透视数据前的数据集。  
  
|年|产品名称|总计|  
|----------|------------------|-----------|  
|2004|HL Mountain Tire|1504884.15|  
|2003|Road Tire Tube|35920.50|  
|2004|Water Bottle - 30 oz.|2805.00|  
|2002|Touring Tire|62364.225|  
  
 下表显示对 **年** 列透视数据后的数据集。  
  
||2002|2003|2004|  
|-|----------|----------|----------|  
|HL Mountain Tire|141164.10|446297.775|1504884.15|  
|Road Tire Tube|3592.05|35920.50|89801.25|  
|Water Bottle - 30 oz.|*NULL*|*NULL*|2805.00|  
|Touring Tire|62364.225|375051.60|1041810.00|  
  
 为了如上所示对 **年** 列透视数据，在 **“透视”** 对话框中设置了以下选项。  
  
-   在 **“透视键”** 列表框中选择了“年”。  
  
-   在 **“设置键”** 列表框中选择了“产品名称”。  
  
-   在 **“透视值”** 列表框中选择了“总计”。  
  
-   在 **“根据值生成透视输出列”** 框中输入以下值。  
  
     [2002],[2003],[2004]  
  
## <a name="configuration-of-the-pivot-transformation"></a>透视转换的配置  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 **“高级编辑器”** 对话框中设置的属性的详细信息，请单击下列主题之一：  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [转换自定义属性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-content"></a>相关内容  
 有关如何设置数据流组件属性的信息，请参阅 [设置数据流组件属性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>另请参阅  
 [逆透视转换](../../../integration-services/data-flow/transformations/unpivot-transformation.md)   
 [数据流](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 转换](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
