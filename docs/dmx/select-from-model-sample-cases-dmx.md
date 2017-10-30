---
title: "SELECT FROM&lt;模型&gt;。SAMPLE_CASES (DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SAMPLE_CASES
- SELECT
- FROM
dev_langs:
- DMX
helpviewer_keywords:
- SELECT FROM <model>.SAMPLE_CASES statement
- mining models [Analysis Services], sample cases
- sample cases [DMX]
- training mining models
ms.assetid: e7a34b9b-3562-4503-bfa7-dd9b12db480a
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3c1e90c2d4fd6b7dab565550bc4b08a4a33192ee
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="select-from-ltmodelgtsamplecases-dmx"></a>SELECT FROM&lt;模型&gt;。SAMPLE_CASES (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回示例事例，用于代表为数据挖掘模型定型所用的事例。  
  
 若要使用此语句，必须在创建挖掘模型时启用钻取功能。 有关启用钻取详细信息，请参阅[创建挖掘模型 &#40; DMX &#41;](../dmx/create-mining-model-dmx.md)， [SELECT INTO &#40; DMX &#41;](../dmx/select-into-dmx.md)，和[ALTER MINING STRUCTURE &#40; DMX &#41;](../dmx/alter-mining-structure-dmx.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.SAMPLE_CASES  
[WHERE <condition list>] ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>参数  
 *n*  
 選擇性。 一个指定返回行数的整数。  
  
 *表达式列表*  
 相关列标识符的逗号分隔列表。  
  
 *model*  
 一个模型标识符。  
  
 *条件列表*  
 選擇性。 限制条件，用于限制从列列表返回的值。  
  
 *expression*  
 選擇性。 一个返回标量值的表达式。  
  
## <a name="remarks"></a>備註  
 可能生成样本事例，但其可能并不实际存在于定型数据中。 返回的事例代表指定的内容节点。  
  
 尽管[!INCLUDE[msCoName](../includes/msconame-md.md)]序列聚类分析算法是唯一[!INCLUDE[msCoName](../includes/msconame-md.md)]支持选择从使用的算法\<模型 >。SAMPLE_CASES，第三方算法可能还支持它。  
  
## <a name="examples"></a>示例  
 以下示例可返回为目标邮件挖掘模型定型所用的样本事例。 使用[IsInNode &#40; DMX &#41;](../dmx/isinnode-dmx.md)函数中**其中**子句将返回唯一的用例都与"000000003"节点相关联。 可以在架构行集的 NODE_UNIQUE_NAME 列中找到节点字符串。  
  
```  
Select * from [Sequence Clustering].SAMPLE_Cases  
WHERE IsInNode('000000003')  
```  
  
## <a name="see-also"></a>另请参阅  
 [选择 &#40; DMX &#41;](../dmx/select-dmx.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

