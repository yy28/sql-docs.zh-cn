---
title: PredictAssociation (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7a23407b546bcde2dd1fde81654da4fe861e0719
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37989539"
---
# <a name="predictassociation-dmx"></a>PredictAssociation (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  预测关联的成员身份。  
  
例如，PredictAssociation 函数可用于获取给定客户的购物篮的当前状态的建议的组。 
  
## <a name="syntax"></a>语法  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>适用范围  
 包含可预测嵌套的表，包括关联和某些分类算法的算法。 支持嵌套的表的分类算法包括[!INCLUDE[msCoName](../includes/msconame-md.md)]决策树[!INCLUDE[msCoName](../includes/msconame-md.md)]Naive Bayes 和[!INCLUDE[msCoName](../includes/msconame-md.md)]神经网络算法。  
  
## <a name="return-type"></a>返回类型  
 \<表表达式 >  
  
## <a name="remarks"></a>Remarks  
 选项**PredictAssociation**函数包括 EXCLUDE_NULL、 INCLUDE_NULL、 INCLUSIVE、 EXCLUSIVE （默认值）、 INPUT_ONLY、 INCLUDE_STATISTICS 和 INCLUDE_NODE_ID。  
  
> [!NOTE]  
>  INCLUSIVE、EXCLUSIVE、INPUT_ONLY 和 INCLUDE_STATISTICS 只适用于表列引用；EXCLUDE_NULL 和 INCLUDE_NULL 只适用于标量列引用。  
  
 INCLUDE_STATISTICS 只返回 **$Probability**并 **$AdjustedProbability**。  
  
 如果数值参数*n*指定，则**PredictAssociation**函数将返回基于概率的前 n 个最可能值：  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 如果包括 **$AdjustedProbability**，该语句返回前*n*值基于 **$AdjustedProbability**。  
  
## <a name="examples"></a>示例  
 下面的示例使用**PredictAssociation**函数返回的四个产品在 Adventure Works 数据库的最有可能一起销售。  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
下面的示例演示如何使用嵌套的表作为预测函数中，输入使用 SHAPE 子句。 SHAPE 查询使用 customerId 作为一个列和嵌套的表作为第二列，其中包含的客户都已带来的产品列表创建行集。 

~~~~
SELECT T.[CustomerId], PredictAssociation(MyNestedTable, 5) // returns top 5 associated items
FROM My Model
PREDICTION JOIN
SHAPE {
    OPENQUERY([Adventure Works DW],'SELECT CustomerID, OrderNumber
    FROM vAssocSeqOrders ORDER BY OrderNumber')
} APPEND (
    {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, model FROM 
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}
  RELATE OrderNumber to OrderNumber) AS T
~~~~  

  
## <a name="see-also"></a>请参阅  
 [数据挖掘扩展插件&#40;DMX&#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [通用预测函数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
