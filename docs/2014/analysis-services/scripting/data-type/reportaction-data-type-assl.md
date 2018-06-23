---
title: ReportAction 数据类型 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ReportAction Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ReportAction
helpviewer_keywords:
- ReportAction data type
ms.assetid: b22f0d52-ed3a-4239-840e-0eaf172d7276
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7c2c5140f3d2723f0456b007bc9228c5f87bbaa6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024905"
---
# <a name="reportaction-data-type-assl"></a>ReportAction 数据类型 (ASSL)
  定义一个派生的数据类型，表示生成的操作[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]报表。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ReportAction>  
   <!-- The following elements extend Action -->  
   <ReportServer>...</ReportServer>  
   <Path>...</Path>  
   <ReportParameters>...</ReportParameters>  
   <ReportFormatParameters>...</ReportFormatParameters>  
</ReportAction>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|[操作](action-data-type-assl.md)|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[路径](../properties/path-element-assl.md)， [ReportFormatParameters](../collections/reportformatparameters-element-assl.md)， [ReportParameters](../collections/reportparameters-element-assl.md)， [ReportServer](../objects/server-element-assl.md)|  
|派生元素|[操作](../objects/action-element-assl.md)([操作](../collections/actions-element-assl.md)集合[多维数据集](../objects/cube-element-assl.md)或[透视](../objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 报表服务器会对基于 URL 的报表请求作出响应。 使用类型定义的报表操作*报表*。 创建操作时，会将资源和参数发送到服务器。 服务器会将该操作公开为类型行集的操作。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ReportAction>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  