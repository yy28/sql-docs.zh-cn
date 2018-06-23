---
title: Multilookup 函数（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1fec079e-33b3-4e4d-92b3-6b4d06a49a77
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 92395b7b91d94187dc790978baa084c418224686
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129134"
---
# <a name="multilookup-function-report-builder-and-ssrs"></a>Multilookup 函数（报表生成器和 SSRS）
  从包含名称/值对的数据集返回指定名称集的一组第一个匹配值。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>语法  
  
```  
  
Multilookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>Parameters  
 *source_expression*  
 (`VariantArray`)，当前作用域中计算且指定的名称或键用于查找组的表达式。 例如，对于多值参数， `=Parameters!IDs.value`。  
  
 *destination_expression*  
 (`Variant`) 针对数据集中的每行计算结果并指定要匹配的名称或键的表达式。 例如， `=Fields!ID.Value`。  
  
 *result_expression*  
 (`Variant`) 计算数据集中的行的表达式其中*source_expression* = *destination_expression*，并指定要检索的值。 例如， `=Fields!Name.Value`。  
  
 *数据集 (dataset)*  
 指定报表中数据集的名称的常量。 例如，“Colors”。  
  
## <a name="return"></a>返回  
 返回`VariantArray`，或`Nothing`如果没有匹配项。  
  
## <a name="remarks"></a>Remarks  
 使用`Multilookup`从其中每个对具有 1 对 1 关系的名称-值对的数据集检索一组值。 `MultiLookup` 等效于调用`Lookup`一组的名称或键。 例如，对于基于主键标识符的多值参数，可以使用`Multilookup`中的表达式中用于检索其关联的值的未绑定到该参数或表的数据集的表中的文本框。  
  
 `Multilookup` 执行以下任务：  
  
-   计算当前作用域中源表达式的结果并生成变体对象的数组。  
  
-   对于数组中的每个对象，调用 [Lookup 函数（报表生成器和 SSRS）](report-builder-functions-lookup-function.md)并向返回数组添加结果。  
  
-   返回结果集。  
  
 若要从具有指定名称的名称/值对（具有 1 对 1 的关系）的数据集中检索单个值，请使用 [Lookup 函数（报表生成器和 SSRS）](report-builder-functions-lookup-function.md)。 若要从具有某名称的名称-值对（具有 1 对多的关系）的数据集中检索多个值，请使用 [LookupSet 函数（报表生成器和 SSRS）](report-builder-functions-lookupset-function.md)。  
  
 存在下列限制：  
  
-   `Multilookup` 在应用所有筛选表达式后计算  
  
-   只支持一个级别的查找。 源、目标或结果表达式不能包含对查找函数的引用。  
  
-   源和目标表达式必须对同一数据类型计算结果。  
  
-   源、目标和结果表达式不能包含对报表或组变量的引用。  
  
-   `Multilookup` 不能用作表达式以下报表项：  
  
    -   数据源的动态连接字符串。  
  
    -   数据集中的计算字段。  
  
    -   数据集中的查询参数。  
  
    -   数据集中的筛选器。  
  
    -   报表参数。  
  
    -   Report.Language 属性。  
  
 有关详细信息，请参阅[聚合函数引用（报表生成器和 SSRS）](report-builder-functions-aggregate-functions-reference.md)和[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="example"></a>示例  
 假定名为“Category”的数据集包含字段 CategoryList，该字段包含类别标识符的逗号分隔列表，例如“2, 4, 2, 1”。  
  
 数据集 CategoryNames 包含类别标识符和类别名称，如下表中所示：  
  
|ID|“属性”|  
|--------|----------|  
|@shouldalert|Accessories|  
|2|Bikes|  
|3|Clothing|  
|4|组件|  
  
 若要查找与标识符列表对应的名称，请使用 `Multilookup`。 你必须首先将列表拆分为字符串数组，调用`Multilookup`检索类别名称，并将结果串联起来成一个字符串。  
  
 将以下表达式放入绑定到 Category 数据集的数据区域中的文本框时，显示“自行车, 组件, 自行车, 附件”：  
  
```  
=Join(MultiLookup(Split(Fields!CategoryList.Value,","),  
   Fields!CategoryID.Value,Fields!CategoryName.Value,"Category")),  
   ", ")  
```  
  
## <a name="example"></a>示例  
 假定数据集 ProductColors 包含颜色标识符字段 ColorID 和颜色值字段 Color，如下表中所示：  
  
|ColorID|Color|  
|-------------|-----------|  
|@shouldalert|Red|  
|2|蓝色|  
|3|绿色|  
  
 假定多值参数 *MyColors* 未绑定到数据集以获取可用值。 该参数的默认值设置为 2 和 3。 将以下表达式放入表中的文本框时，将该参数的多个所选值连接为逗号分隔的列表并显示“蓝色, 绿色”。  
  
```  
=Join(MultiLookup(Parameters!MyColors.Value,Fields!ColorID.Value,Fields!Color.Value,"ProductColors"),", ")  
```  
  
## <a name="see-also"></a>请参阅  
 [在报表中使用表达式&#40;报表生成器和 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)   
 [总计、 聚合和内置集合的表达式作用域&#40;报表生成器和 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  