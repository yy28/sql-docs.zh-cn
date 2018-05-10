---
title: Level 函数（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 41235402-bb9e-4cb7-b91e-431e77db19cf
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e092b79a5ddd1e43a740520fc2505cc0dede5b4d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="report-builder-functions---level-function"></a>报表生成器函数 - Level 函数
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
 返回 **Integer**。 如果 scope 指定数据集或数据区域，或指定非递归分组（即没有父元素的分组），则 Level 返回 0。 如果省略 *scope* ，则返回当前作用域的级别。  
  
## <a name="remarks"></a>Remarks  
 **Level** 函数返回的值从 0 开始；即，层次结构中的第一级为 0。  
  
 **Level** 函数可用于为递归层次结构（如雇员列表）提供缩进格式。  
  
 有关递归层次结构的详细信息，请参阅[创建递归层次结构组（报表生成器和 SSRS）](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
## <a name="example"></a>示例  
 下面的代码示例提供了 Employees 组中行的级别：  
  
```  
=Level("Employees")  
```  
  
## <a name="see-also"></a>另请参阅  
 [在报表中使用表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
