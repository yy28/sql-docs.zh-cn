---
title: ReportAction 数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eb1679d0275e6662116976b572f612f9ab113bb1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164307"
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
|派生数据类型|None|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[路径](../properties/path-element-assl.md)， [ReportFormatParameters](../collections/reportformatparameters-element-assl.md)， [ReportParameters](../collections/reportparameters-element-assl.md)， [ReportServer](../objects/server-element-assl.md)|  
|派生元素|[操作](../objects/action-element-assl.md)([操作](../collections/actions-element-assl.md)的集合[多维数据集](../objects/cube-element-assl.md)或[角度来看](../objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>备注  
 报表服务器会对基于 URL 的报表请求作出响应。 报表操作定义的类型*报表*。 创建操作时，会将资源和参数发送到服务器。 服务器会将该操作公开为类型行集的操作。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ReportAction>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
