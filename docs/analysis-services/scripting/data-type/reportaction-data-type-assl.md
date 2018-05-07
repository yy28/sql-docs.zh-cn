---
title: ReportAction 数据类型 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eb74ce436b7c10882f6ccad822684e782066f636
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="reportaction-data-type-assl"></a>ReportAction 数据类型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 [Analysis Services 脚本语言 XML 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
