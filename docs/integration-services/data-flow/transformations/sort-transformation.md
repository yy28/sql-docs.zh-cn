---
title: 排序转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sorttrans.f1
- sql13.dts.designer.sorttransformation.f1
helpviewer_keywords:
- Sort transformation
- descending sorts
- ascending sorts
- sorting data [Integration Services]
- multiple sorts
- duplicate data [Integration Services]
ms.assetid: 728c9351-84a8-4a89-be4d-d50d4adc04e0
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a20feb9d15a24ea417a715816e3b437e13d0ca2c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sort-transformation"></a>排序转换
  排序转换按升序或降序对输入数据进行排序，并将排序后的数据复制到转换输出。 您可以对一个输入应用多个排序；每个排序都由确定排序顺序的一个数字来标识。 首先对具有最小数字的列进行排序，然后对具有第二小数字的排序列进行排序，依此类推。 例如，如果名为 **CountryRegion** 的列的排序顺序为 1，而名为 **City** 的列的排序顺序为 2，则输出先按照 country/region（国家/地区）排序，然后按照 city（城市）排序。 正数表示排序为升序排序，负数表示排序为降序排序。 不进行排序的列的排序顺序为 0。 没有选择进行排序的列将与被排序列一起自动被复制到转换输出。  
  
 排序转换包含一组比较选项，这些选项可以定义转换处理列中字符串数据的方式。 有关详细信息，请参阅 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)。  
  
> [!NOTE]  
>  排序转换对 GUID 进行排序的顺序不同于 ORDER BY 子句在 Transact-SQL 中对其排序的顺序。 排序转换先对以 0-9 开头的 GUID 进行排序，然后再对以 A-F 开头的 GUID 进行排序，而 ORDER BY 子句对 GUID 进行排序的顺序则不同于此，这在 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]中得到了体现。 有关详细信息，请参阅 [ORDER BY 子句 (Transact-SQL)](../../../t-sql/queries/select-order-by-clause-transact-sql.md)。  
  
 作为排序操作的一部分，排序转换还可删除重复行。 重复行是具有相同排序键值的行。 排序键值是根据所用的字符串比较选项生成的，这意味着不同文字字符串可能具有相同的排序键值。 转换将输入列中具有不同值但具有相同排序键的行标识为重复行。  
  
 排序转换包括了可以在加载包时通过属性表达式进行更新的 **MaximumThreads** 自定义属性。 有关详细信息，请参阅 [Integration Services (SSIS) 表达式](../../../integration-services/expressions/integration-services-ssis-expressions.md)、[在包中使用属性表达式](../../../integration-services/expressions/use-property-expressions-in-packages.md)和[转换自定义属性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)。  
  
 此转换有一个输入和一个输出。 它不支持错误输出。  
  
## <a name="configuration-of-the-sort-transformation"></a>排序转换的配置  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [转换自定义属性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何设置组件属性的详细信息，请参阅 [设置数据流组件属性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="related-content"></a>相关内容  
 codeplex.com 上的示例 [SortDeDuplicateDelimitedString 自定义 SSIS 组件](http://go.microsoft.com/fwlink/?LinkId=220821)。  
  
## <a name="sort-transformation-editor"></a>排序转换编辑器
  可以使用 **“排序转换编辑器”** 对话框，选择要排序的列，设置排序顺序以及指定是否删除重复项。  
  
### <a name="options"></a>“常规”  
 **可用输入列**  
 使用此复选框可以指定要排序的列。  
  
 **名称**  
 查看每个可用输入列的名称。  
  
 **传递**  
 指示是否在排序输出中包含相应列。  
  
 **输入列**  
 从每行的可用输入列的列表中选择。 通过选中 **“可用输入列”** 表中的复选框来选择列。  
  
 **输出别名**  
 为每个输出列键入一个别名。 默认值为输入列的名称；不过，您也可以任选一个唯一的描述性名称。  
  
 **排序类型**  
 指示按升序还是按降序排序。  
  
 **排序顺序**  
 指示列的排序顺序。 必须对每列手动设置此选项。  
  
 **比较标志**  
 有关字符串比较选项的信息，请参阅 [比较字符串数据](../../../integration-services/data-flow/comparing-string-data.md)。  
  
 **删除具有重复排序值的行**  
 根据指定的字符串比较选项，指示转换是将重复行复制到转换输出，还是为所有重复项创建单个条目。  
  
## <a name="see-also"></a>另请参阅  
 [数据流](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 转换](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
