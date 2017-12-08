---
title: "ReportAction 数据类型 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ReportAction Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ReportAction
helpviewer_keywords: ReportAction data type
ms.assetid: b22f0d52-ed3a-4239-840e-0eaf172d7276
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2d88cfbf36d07dec984d38712b8e5ab893d811a5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
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
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|[操作](../../../analysis-services/scripting/data-type/action-data-type-assl.md)|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[路径](../../../analysis-services/scripting/properties/path-element-assl.md)， [ReportFormatParameters](../../../analysis-services/scripting/collections/reportformatparameters-element-assl.md)， [ReportParameters](../../../analysis-services/scripting/collections/reportparameters-element-assl.md)， [ReportServer](../../../analysis-services/scripting/properties/reportserver-element-assl.md)|  
|派生元素|[操作](../../../analysis-services/scripting/objects/action-element-assl.md)([操作](../../../analysis-services/scripting/collections/actions-element-assl.md)集合[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)或[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>注释  
 报表服务器会对基于 URL 的报表请求作出响应。 使用类型定义的报表操作*报表*。 创建操作时，会将资源和参数发送到服务器。 服务器会将该操作公开为类型行集的操作。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ReportAction>。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
