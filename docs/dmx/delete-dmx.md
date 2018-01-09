---
title: "删除 (DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: DELETE
dev_langs: DMX
helpviewer_keywords:
- DELETE statement [DMX]
- mining structures [DMX], clearing
- clearing mining models
- deleting mining models
- mining models [Analysis Services], clearing
- deleting mining structures
ms.assetid: 5a8204c3-a3df-4d97-9c1d-d997d24c70e3
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 566ae835ad06e99edbf624ab6d25611c0a8427f7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
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
  
 有关处理类型的详细信息，请参阅[类型元素 &#40;XMLA &#41;](../analysis-services/xmla/xml-elements-properties/type-element-xmla.md).  
  
## <a name="examples"></a>示例  
 下面的示例将删除 NB_Sample 模型中的所有内容。  
  
```  
DELETE FROM NB_Sample.CONTENT  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40; DMX &#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
