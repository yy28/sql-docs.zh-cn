---
title: 程序集的数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Assembly Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Assembly data type
ms.assetid: 0a381322-9509-4579-a754-c6cdd0a70cc9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eb02963baa8a7fca296abe89801d89c1f7ea19fa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48209634"
---
# <a name="assembly-data-type-assl"></a>Assembly 数据类型 (ASSL)
  定义表示一个抽象的基元数据类型[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]程序集或 COM 动态链接库 (DLL) 与相关联[服务器](../objects/server-element-assl.md)或[数据库](../objects/database-element-assl.md)元素。  
  
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
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|None|  
|派生数据类型|[ClrAssembly](assembly-data-type-assl.md)， [ComAssembly](comassembly-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[批注](../collections/annotations-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)，[说明](../properties/description-element-assl.md)， [ID](../properties/id-element-assl.md)， [ImpersonationInfo](../properties/impersonationinfo-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)，[名称](../properties/name-element-assl.md)|  
|派生元素|None|  
  
## <a name="remarks"></a>备注  
 `Assembly` 数据类型可作为 `ComAssembly` 元素的基本数据类型，该元素表示与实例或数据库关联的 COM 库；还可作为 `ClrAssembly` 元素的基本数据类型，该元素表示与实例或数据库关联的 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 程序集。 有关程序集的详细信息，请参阅[多维模型程序集管理](../../multidimensional-models/multidimensional-model-assemblies-management.md)。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Assembly>。  
  
## <a name="see-also"></a>请参阅  
 [服务器元素&#40;ASSL&#41;](../objects/server-element-assl.md)   
 [数据库元素&#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
