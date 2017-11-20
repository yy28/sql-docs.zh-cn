---
title: "PredictAssociation (DMX) |Microsoft 文档"
ms.custom: 
ms.date: 09/14/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PredictAssociation
dev_langs:
- DMX
helpviewer_keywords:
- PredictAssociation function
ms.assetid: 33eb66b5-84c6-449f-aaae-316345bc4ad5
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1fcebadb217b3ecbf2de828cc9566f4af5ffeddd
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="predictassociation-dmx"></a>PredictAssociation (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  预测关联的成员身份。  
  
例如，PredictAssociation 函数可用于获取组为客户提供的购物篮的当前状态的建议。 
  
## <a name="syntax"></a>语法  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>适用范围  
 包含可预测的嵌套的表，包括关联和某些分类算法的算法。 支持嵌套的表的分类算法包括[!INCLUDE[msCoName](../includes/msconame-md.md)]决策树[!INCLUDE[msCoName](../includes/msconame-md.md)]Naive Bayes 和[!INCLUDE[msCoName](../includes/msconame-md.md)]神经网络算法。  
  
## <a name="return-type"></a>返回类型  
 \<表表达式 >  
  
## <a name="remarks"></a>注释  
 选项**PredictAssociation**函数包括 EXCLUDE_NULL、 INCLUDE_NULL、 非独占时间、 独占 （默认值）、 INPUT_ONLY、 INCLUDE_STATISTICS 和 INCLUDE_NODE_ID。  
  
> [!NOTE]  
>  INCLUSIVE、EXCLUSIVE、INPUT_ONLY 和 INCLUDE_STATISTICS 只适用于表列引用；EXCLUDE_NULL 和 INCLUDE_NULL 只适用于标量列引用。  
  
 仅返回 INCLUDE_STATISTICS **$Probability**和**$AdjustedProbability**。  
  
 如果数值参数 *n* 指定，则**PredictAssociation**函数返回的概率在基于的前 n 最有可能值：  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 如果包含**$AdjustedProbability**，该语句返回顶部 *n* 值基于**$AdjustedProbability**。  
  
## <a name="examples"></a>示例  
 下面的示例使用**PredictAssociation**函数以返回四个产品的 Adventure Works 数据库是最有可能一起销售。  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
下面的示例演示如何使用嵌套的表作为预测函数中，输入使用形状子句。 SHAPE 查询创建行集作为一个列的 customerId 和嵌套的表作为第二个列，包含了已到客户的产品的列表。 

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
 [数据挖掘扩展插件 &#40; DMX &#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [常规预测函数 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

