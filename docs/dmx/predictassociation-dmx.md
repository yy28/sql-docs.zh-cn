---
title: PredictAssociation （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ea0a9915e062d7b6f15b63e18976e88cc339202d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "76939499"
---
# <a name="predictassociation-dmx"></a>PredictAssociation (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  预测关联的成员身份。  
  
例如，你可以使用 PredictAssociation 函数获取客户的购物篮当前状态提供的一组建议。 
  
## <a name="syntax"></a>语法  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>应用于  
 包含可预测的嵌套表（包括关联和某些分类算法）的算法。 支持嵌套表的[!INCLUDE[msCoName](../includes/msconame-md.md)]分类算法包括决策树、 [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes 和[!INCLUDE[msCoName](../includes/msconame-md.md)]神经网络算法。  
  
## <a name="return-type"></a>返回类型  
 \<表表达式>  
  
## <a name="remarks"></a>备注  
 **PredictAssociation**函数的选项包括 EXCLUDE_NULL、INCLUDE_NULL、包含、异（默认）、INPUT_ONLY、INCLUDE_STATISTICS 和 INCLUDE_NODE_ID。  
  
> [!NOTE]  
>  INCLUSIVE、EXCLUSIVE、INPUT_ONLY 和 INCLUDE_STATISTICS 只适用于表列引用；EXCLUDE_NULL 和 INCLUDE_NULL 只适用于标量列引用。  
  
 INCLUDE_STATISTICS 仅返回 **$Probability**和 **$AdjustedProbability**。  
  
 如果指定了数字参数*n* ，则**PredictAssociation**函数将根据概率返回前 n 个最可能的值：  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 如果包括 **$AdjustedProbability**，则该语句将返回基于 **$AdjustedProbability**的前*n*个值。  
  
## <a name="examples"></a>示例  
 下面的示例使用**PredictAssociation**函数返回艾德公司数据库中最有可能一起销售的四个产品。  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
下面的示例演示如何使用 SHAPE 子句将嵌套表用作预测函数的输入。 SHAPE 查询将 customerId 作为一个列创建，并将嵌套表作为第二列创建，其中包含客户已经提供的产品的列表。 

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

  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的常规预测函数](../dmx/general-prediction-functions-dmx.md)  
  
  
