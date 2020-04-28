---
title: 删除（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c1c75a6ff18b26bee65365acbc068de87678a9c7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68070757"
---
# <a name="delete-dmx"></a>DELETE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  根据使用的数据挖掘扩展插件 (DMX) 子句，清除挖掘模型、挖掘结构或挖掘结构以及所有关联的挖掘模型。  
  
## <a name="syntax"></a>语法  
  
```  
  
DELETE FROM [MINING MODEL] <model>[.CONTENT]  
DELETE FROM [MINING STRUCTURE] <structure>[.CONTENT]|[.CASES]  
```  
  
## <a name="arguments"></a>参数  
 *模型*  
 模型标识符。  
  
 *构造*  
 结构标识符。  
  
## <a name="remarks"></a>备注  
 如果未指定**挖掘模型**或**挖掘结构**， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]将根据名称搜索对象类型，并处理正确的对象。 如果服务器包含同名的挖掘结构和挖掘模型，将返回错误。  
  
 下表说明了使用不同形式的语法所产生的结果。  
  
|语句|结果|  
|---------------|------------|  
|从挖掘结构*\<结构中删除>*<br /><br /> 或<br /><br /> 从挖掘结构*\<结构>* 删除。CONTENT|对挖掘结构执行 ProcessClear。 从挖掘结构及其关联的挖掘模型中清除所有内容。|  
|从挖掘结构*\<结构>* 删除。这|对挖掘结构执行 ProcessClearStructureOnly。 从挖掘结构中清除所有内容，但不改变与其关联的挖掘模型。 清除挖掘结构后，将无法钻取关联的挖掘模型。|  
|从挖掘模型*\<模型中删除>*<br /><br /> 或<br /><br /> 从挖掘模型*\<模型>* 删除。CONTENT|对挖掘模型执行 ProcessClear，但保持状态值不变。 状态值是列的可能状态。 例如，性别列的状态值是男性和女性。|  
  
 有关处理类型的详细信息，请参阅[Type Element &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla)。  
  
## <a name="examples"></a>示例  
 下面的示例将删除 NB_Sample 模型中的所有内容。  
  
```  
DELETE FROM NB_Sample.CONTENT  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
