---
title: 删除 (DMX) |Microsoft 文档
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e5b11bda21fe877af419442cb8b98acd4d29c21b
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841270"
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
 *model*  
 一个模型标识符。  
  
 *结构*  
 结构标识符。  
  
## <a name="remarks"></a>Remarks  
 如果不指定**挖掘模型**或**挖掘结构**，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]搜索依据的名称，该对象类型并处理正确的对象。 如果服务器包含同名的挖掘结构和挖掘模型，将返回错误。  
  
 下表说明了使用不同形式的语法所产生的结果。  
  
|。|结果|  
|---------------|------------|  
|DELETE FROM MINING STRUCTURE*\<结构 >*<br /><br /> 或多个<br /><br /> DELETE FROM MINING STRUCTURE*\<结构 >*。内容|执行 ProcessClear 对挖掘结构。 从挖掘结构及其关联的挖掘模型中清除所有内容。|  
|DELETE FROM MINING STRUCTURE*\<结构 >*。用例|执行 ProcessClearStructureOnly 对挖掘结构。 从挖掘结构中清除所有内容，但不改变与其关联的挖掘模型。 清除挖掘结构后，将无法钻取关联的挖掘模型。|  
|删除从挖掘模型*\<模型 >*<br /><br /> 或多个<br /><br /> 删除从挖掘模型*\<模型 >*。内容|对挖掘模型执行 ProcessClear 但使状态的值保持不变。 状态值是列的可能状态。 例如，性别列的状态值是男性和女性。|  
  
 有关处理类型的详细信息，请参阅[类型元素&#40;XMLA&#41;](../analysis-services/xmla/xml-elements-properties/type-element-xmla.md)。  
  
## <a name="examples"></a>示例  
 下面的示例将删除 NB_Sample 模型中的所有内容。  
  
```  
DELETE FROM NB_Sample.CONTENT  
```  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘扩展插件&#40;DMX&#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件&#40;DMX&#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
