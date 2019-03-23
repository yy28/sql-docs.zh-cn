---
title: 排序转换 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sorttrans.f1
helpviewer_keywords:
- Sort transformation
- descending sorts
- ascending sorts
- sorting data [Integration Services]
- multiple sorts
- duplicate data [Integration Services]
ms.assetid: 728c9351-84a8-4a89-be4d-d50d4adc04e0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dba1f3598abb8877721ff77d3dabcc8af8e0b94a
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374415"
---
# <a name="sort-transformation"></a>排序转换
  排序转换按升序或降序对输入数据进行排序，并将排序后的数据复制到转换输出。 您可以对一个输入应用多个排序；每个排序都由确定排序顺序的一个数字来标识。 首先对具有最小数字的列进行排序，然后对具有第二小数字的排序列进行排序，依此类推。 例如，如果名为 **CountryRegion** 的列的排序顺序为 1，而名为 **City** 的列的排序顺序为 2，则输出先按照 country/region（国家/地区）排序，然后按照 city（城市）排序。 正数表示排序为升序排序，负数表示排序为降序排序。 不进行排序的列的排序顺序为 0。 没有选择进行排序的列将与被排序列一起自动被复制到转换输出。  
  
 排序转换包含一组比较选项，这些选项可以定义转换处理列中字符串数据的方式。 有关详细信息，请参阅 [Comparing String Data](../comparing-string-data.md)。  
  
> [!NOTE]  
>  排序转换对 GUID 进行排序的顺序不同于 ORDER BY 子句在 Transact-SQL 中对其排序的顺序。 排序转换先对以 0-9 开头的 GUID 进行排序，然后再对以 A-F 开头的 GUID 进行排序，而 ORDER BY 子句对 GUID 进行排序的顺序则不同于此，这在 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]中得到了体现。 有关详细信息，请参阅 [ORDER BY 子句 (Transact-SQL)](/sql/t-sql/queries/select-order-by-clause-transact-sql)。  
  
 作为排序操作的一部分，排序转换还可删除重复行。 重复行是具有相同排序键值的行。 排序键值是根据所用的字符串比较选项生成的，这意味着不同文字字符串可能具有相同的排序键值。 转换将输入列中具有不同值但具有相同排序键的行标识为重复行。  
  
 排序转换包括了可以在加载包时通过属性表达式进行更新的 `MaximumThreads` 自定义属性。 有关详细信息，请参阅 [Integration Services (SSIS) 表达式](../../expressions/integration-services-ssis-expressions.md)、[在包中使用属性表达式](../../expressions/use-property-expressions-in-packages.md)和[转换自定义属性](transformation-custom-properties.md)。  
  
 此转换有一个输入和一个输出。 它不支持错误输出。  
  
## <a name="configuration-of-the-sort-transformation"></a>排序转换的配置  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可在 **“排序转换编辑器”** 对话框中设置的属性的信息，请参阅 [Sort Transformation Editor](../../sort-transformation-editor.md)。  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](../../common-properties.md)  
  
-   [转换自定义属性](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何设置组件属性的详细信息，请参阅 [设置数据流组件属性](../set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="related-content"></a>相关内容  
 codeplex.com 上的示例 [SortDeDuplicateDelimitedString 自定义 SSIS 组件](https://go.microsoft.com/fwlink/?LinkId=220821)。  
  
## <a name="see-also"></a>请参阅  
 [数据流](../data-flow.md)   
 [Integration Services 转换](integration-services-transformations.md)  
  
  
