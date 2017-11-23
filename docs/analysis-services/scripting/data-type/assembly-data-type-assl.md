---
title: "程序集的数据类型 (ASSL) |Microsoft 文档"
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
apiname: Assembly Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: Assembly data type
ms.assetid: 0a381322-9509-4579-a754-c6cdd0a70cc9
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d3c8d9ad46dd000a6a2ff6a6e89b656028771fdc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="assembly-data-type-assl"></a>Assembly 数据类型 (ASSL)
  定义表示的抽象基元数据类型[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]程序集或 COM 动态链接库 (DLL) 与关联[服务器](../../../analysis-services/scripting/objects/server-element-assl.md)或[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。  
  
> [!IMPORTANT]  
>  COM 程序集可能会造成安全风险。 由于此风险和其他注意事项， [!INCLUDE[ssASversion10](../../../includes/ssasversion10-md.md)]中不推荐使用 COM 程序集。 未来版本可能不支持 COM 程序集。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Assembly>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Description>...</Description>  
   <CreatedTimestamp>...</CreatedTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <ImpersonationInfo>...</ImpersonationInfo>  
   <Annotations>...</Annotations>  
</Assembly>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|无|  
|派生数据类型|[ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)， [ComAssembly](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)，[说明](../../../analysis-services/scripting/properties/description-element-assl.md)， [ID](../../../analysis-services/scripting/properties/id-element-assl.md)， [ImpersonationInfo](../../../analysis-services/scripting/properties/impersonationinfo-element-assl.md)， [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)，[名称](../../../analysis-services/scripting/properties/name-element-assl.md)|  
|派生元素|无|  
  
## <a name="remarks"></a>注释  
 **程序集**数据类型用作的基本数据类型**ComAssembly**元素，它表示与实例或数据库关联的 COM 库，与**ClrAssembly**元素，它表示[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]与实例或数据库相关联的程序集。 有关程序集的详细信息，请参阅[多维模型程序集管理](../../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Assembly>。  
  
## <a name="see-also"></a>另请参阅  
 [服务器元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [数据库元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
