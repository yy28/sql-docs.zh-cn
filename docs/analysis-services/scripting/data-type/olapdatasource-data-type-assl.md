---
title: "OlapDataSource 数据类型 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: OlapDataSource Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: OlapDataSource
helpviewer_keywords: OlapDataSource data type
ms.assetid: cfe8937c-5f73-4773-a1e8-5e3310691966
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 46ca5b5c583a0fc1f5a3c38e112804a174432475
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="olapdatasource-data-type-assl"></a>OlapDataSource 数据类型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定义一个派生的数据类型，表示多维[数据源](../../../analysis-services/scripting/objects/datasource-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<OlapDataSource>  
   <!-- Child elements are only those inherited from DataSource -->  
</OlapDataSource>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|[数据源](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|InclusionThresholdSetting|  
|派生元素|[数据源](../../../analysis-services/scripting/objects/datasource-element-assl.md)([数据源](../../../analysis-services/scripting/collections/datasources-element-assl.md)集合[数据库](../../../analysis-services/scripting/objects/database-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.OlapDataSource>。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
