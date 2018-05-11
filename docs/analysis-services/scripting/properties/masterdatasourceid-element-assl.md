---
title: MasterDatasourceID 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: dfa3ee83ddd643577c56dd5569eccb65c67bab78
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="masterdatasourceid-element-assl"></a>MasterDatasourceID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含主数据源标识符 (ID)[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Database>  
   ...  
   <MasterDatasourceID>...</MasterDatasourceID>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 远程实例上的数据库[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]包含远程分区， **MasterDatasourceID**元素包含的数据源 ID 用于标识主数据源实例[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，管理远程分区。  
  
 对应于的父元素**MasterDatasourceID**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Database>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
