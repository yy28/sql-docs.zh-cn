---
title: "聚合函数（报表生成器和 SSRS）| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 16ce643f-bbb3-40a5-ba78-7aed73156f3e
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: a1d7035d148f104a7661f2741c8e3ad6bac2a2ca
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="report-builder-functions---aggregate-function"></a>报表生成器函数 - 聚合函数
  按照数据访问接口的定义返回指定表达式的自定义聚合。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>语法  
  
```  
  
Aggregate(expression, scope)  
```  
  
#### <a name="parameters"></a>Parameters  
 *expression*  
 要对其执行聚合的表达式。 该表达式必须是简单字段引用表达式。  
  
 *作用域*  
 (**String**) 包含要对其应用聚合函数的报表项的数据集、组或数据区域的名称。 *Scope* 必须是字符串常量，且不能是表达式。 如果未指定 *scope* ，则使用当前作用域。  
  
## <a name="return-type"></a>返回类型  
 返回类型视数据访问接口而定。 如果数据访问接口不支持此函数或数据不可用，则返回 **Nothing** 。  
  
## <a name="remarks"></a>Remarks  
 **Aggregate** 函数提供一种方式来使用对外部数据源计算的聚合。 是否支持此功能由数据扩展插件决定。 例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据处理扩展插件从 MDX 查询中检索平展行集。 结果集中的某些行可能包含在数据源服务器上计算的聚合值。 这些聚合值称为“服务器聚合” 。 若要在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的图形查询设计器中查看服务器聚合，可以使用工具栏上的 **“显示聚合”** 按钮。 有关详细信息，请参阅 [Analysis Services MDX 查询设计器用户界面（报表生成器）](http://msdn.microsoft.com/library/7e288eee-2d37-485e-a6a0-dbba5e041e26)。  
  
 在 Tablix 数据区域的详细信息行中显示聚合和详细信息数据集值的组合时，服务器聚合通常不会包括在内，因为它们不是详细信息数据。 但是，您可能希望显示从该数据集中检索到的所有值，并自定义聚合数据的计算方式和显示方式。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 将检测在报表的表达式中使用 **Aggregate** 函数的情况，以便确定是否在详细信息行显示服务器聚合。 如果在数据区域中的表达式中包含 **Aggregate** ，服务器聚合只能出现在组总计行或总计行中，而不会出现在详细信息行中。 如果您希望在详细信息行中显示服务器聚合，请不要使用 **Aggregate** 函数。  
  
 可以通过更改 **“将小计行解释为详细信息”** 选项（位于 **“数据集属性”** 对话框）的值，来更改此默认行为。 此选项设置为 **True**时，包括服务器聚合在内的所有数据都会显示为详细信息数据。 当设置为 **False**时，服务器聚合显示为总计。 此属性的设置影响链接到此数据集的所有数据区域。  
  
> [!NOTE]  
>  引用 **Aggregate** 的报表项所包含的所有组都必须具有其组表达式的简单字段引用，例如， `[FieldName]`。 您不能在使用复杂组表达式的数据区域中使用 **Aggregate** 。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据处理扩展插件，查询必须包括 **LevelProperty** 类型（而不是 **MemberProperty**类型）的 MDX 字段，才能支持使用 **Aggregate**函数的聚合。  
  
 *Expression* 可以包含对嵌套聚合函数的调用，但具有以下例外和条件：  
  
-   嵌套聚合的*Scope* 必须与外部聚合的作用域相同，或者包含在外部聚合的作用域中。 对于表达式中的所有非重复作用域，一个作用域必须相对所有其他作用域处于子关系中。  
  
-   嵌套聚合的*Scope* 不能为数据集的名称。  
  
-   *Expression* 不得包含 **First**、 **Last**、 **Previous**或 **RunningValue** 函数。  
  
-   *Expression* 不得包含用于指定 *recursive*的嵌套聚合。  
  
 有关详细信息，请参阅[聚合函数引用（报表生成器和 SSRS）](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)和[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 有关递归聚合的详细信息，请参阅[创建递归层次结构组（报表生成器和 SSRS）](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
## <a name="comparing-the-aggregate-and-sum-functions"></a>比较 Aggregate 函数和 Sum 函数  
 **Aggregate** 函数不同于数值聚合函数（例如 **Sum** ），区别在于 **Aggregate** 函数会返回由数据访问接口或数据处理扩展插件计算的值， 而类似于 **Sum** 的数值聚合函数会返回由报表处理器针对由 *scope* 参数确定的数据集中的一组数据所计算的值。 有关详细信息，请参阅[聚合函数引用（报表生成器和 SSRS）](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)中列出的聚合函数。  
  
## <a name="example"></a>示例  
 下面的代码示例显示检索字段 `LineTotal`的服务器聚合的表达式。 该表达式将添加至属于组 `GroupbyOrder`的行的某个单元格中。  
  
```  
=Aggregate(Fields!LineTotal.Value, "GroupbyOrder")  
```  
  
## <a name="see-also"></a>另请参阅  
 [在报表中使用表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
