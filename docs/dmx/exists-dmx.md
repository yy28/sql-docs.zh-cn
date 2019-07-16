---
title: 存在 (DMX) |Microsoft 文档
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8dc21f3eb271f4af880bab6eb4d04726e9f80eaa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074864"
---
# <a name="exists-dmx"></a>Exists (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回 **，则返回 true**如果指定的子查询返回至少有一行。  
  
## <a name="syntax"></a>语法  
  
```  
  
EXISTS(<subquery>)  
```  
  
## <a name="arguments"></a>参数  
 *subquery*  
 SELECT 语句的窗体 SELECT * FROM\<列名称 > [其中\<谓词列表 >]。  
  
## <a name="result-type"></a>结果类型  
 返回 **，则返回 true**如果子查询返回的结果集包含至少一个行; 否则，返回**false**。  
  
## <a name="remarks"></a>备注  
 可以在 EXISTS 前面使用 NOT 关键字：例如 `WHERE NOT EXISTS (<subquery>)`。  
  
 添加到 EXISTS 的子查询参数中的列的列表是无关紧要的；函数仅检查满足条件的行是否存在。  
  
## <a name="examples"></a>示例  
 可使用 EXISTS 和 NOT EXISTS 检查嵌套表中的条件。 这在创建控制定型或测试数据挖掘模型所使用的数据的筛选器时，将很有用。 有关详细信息，请参阅[挖掘模型筛选器（Analysis Services - 数据挖掘）](../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)。  
  
 下面的示例基于`[Association]`挖掘结构和挖掘模型中创建[数据挖掘基础教程](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)。 该查询仅返回其中客户至少购买一个 patch kit 的那些事例。  
  
```  
SELECT * FROM [Association].CASES  
WHERE EXISTS  
(  
SELECT * FROM [v Assoc Seq Line Numbers]  
WHERE [[Model] = 'Patch kit'  
)  
```  
  
 若要查看此查询返回的相同数据的另一个方法是在关联查看器中打开该模型中，右键单击项集**Patch kit = Existing**，选择**钻取**选项，然后选择**仅模型事例**。  
  
## <a name="see-also"></a>请参阅  
 [函数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [模型筛选器语法和示例&#40;Analysis Services-数据挖掘&#41;](../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)  
  
  
