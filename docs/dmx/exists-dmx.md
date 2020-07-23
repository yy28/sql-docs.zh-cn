---
title: Exists （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fdf58a943986dc43f82ef7023b68a2c6168a5518
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971707"
---
# <a name="exists-dmx"></a>Exists (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  如果指定的子查询至少返回一行，则返回**true** 。  
  
## <a name="syntax"></a>语法  
  
```  
  
EXISTS(<subquery>)  
```  
  
## <a name="arguments"></a>参数  
 subquery  
 SELECT 语句，格式为 SELECT * FROM \<column name> [WHERE \<predicate list> ]。  
  
## <a name="result-type"></a>结果类型  
 如果子查询返回的结果集至少包含一行，则返回**true** ;否则，返回**false**。  
  
## <a name="remarks"></a>备注  
 可以在 EXISTS 前面使用 NOT 关键字：例如 `WHERE NOT EXISTS (<subquery>)`。  
  
 添加到 EXISTS 的子查询参数中的列的列表是无关紧要的；函数仅检查满足条件的行是否存在。  
  
## <a name="examples"></a>示例  
 可使用 EXISTS 和 NOT EXISTS 检查嵌套表中的条件。 这在创建控制定型或测试数据挖掘模型所使用的数据的筛选器时，将很有用。 有关详细信息，请参阅[挖掘模型筛选器（Analysis Services - 数据挖掘）](https://docs.microsoft.com/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining)。  
  
 下面的示例基于 `[Association]` 您在[数据挖掘基础教程](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)中创建的挖掘结构和挖掘模型。 该查询仅返回其中客户至少购买一个 patch kit 的那些事例。  
  
```  
SELECT * FROM [Association].CASES  
WHERE EXISTS  
(  
SELECT * FROM [v Assoc Seq Line Numbers]  
WHERE [[Model] = 'Patch kit'  
)  
```  
  
 查看此查询返回的相同数据的另一种方法是在关联查看器中打开该模型，右键单击 "项集**修补工具包 = 现有**"，选择 "**钻取**" 选项，然后选择 "**仅模型事例**"。  
  
## <a name="see-also"></a>另请参阅  
 [函数 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [模型筛选器语法和示例（Analysis Services – 数据挖掘）](https://docs.microsoft.com/analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining)  
  
  
