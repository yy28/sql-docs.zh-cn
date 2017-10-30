---
title: "级别函数 （报表生成器和 SSRS） |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 41235402-bb9e-4cb7-b91e-431e77db19cf
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 171842909a300d0c98fca2a26bbf4567810e8e95
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="report-builder-functions---level-function"></a>报表生成器功能-Level 函数
  返回在递归层次结构中的当前深度级别。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>语法  
  
```  
  
Level(scope)  
```  
  
#### <a name="parameters"></a>Parameters  
 *作用域*  
 (**String**)（可选）。 包含要对其应用聚合函数的报表项的数据集、组或数据区域的名称。 如果未指定 *scope* ，则使用当前作用域。  
  
## <a name="return-type"></a>返回类型  
 返回 **Integer**。 如果*作用域*指定数据集或数据区域中，或指定的非递归分组 (即，没有分组**父**元素)，**级别**返回 0。 如果省略 *scope* ，则返回当前作用域的级别。  
  
## <a name="remarks"></a>注释  
 **Level** 函数返回的值从 0 开始；即，层次结构中的第一级为 0。  
  
 **Level** 函数可用于为递归层次结构（如雇员列表）提供缩进格式。  
  
 有关递归层次结构的详细信息，请参阅[创建递归层次结构组（报表生成器和 SSRS）](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
## <a name="example"></a>示例  
 下面的代码示例提供了 Employees 组中行的级别：  
  
```  
=Level("Employees")  
```  
  
## <a name="see-also"></a>另请参阅  
 [在报表 &#40; 中使用表达式报表生成器和 SSRS &#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [表达式 &#40; 中的数据类型报表生成器和 SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [总计、 聚合和内置集合 &#40; 的表达式作用域报表生成器和 SSRS &#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  

