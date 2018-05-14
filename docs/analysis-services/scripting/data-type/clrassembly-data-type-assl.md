---
title: ClrAssembly 数据类型 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f6fb3493fc7add4ece9ef2d5acacd772d5911ebd
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="clrassembly-data-type-assl"></a>ClrAssembly 数据类型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义一个派生的数据类型，表示[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]与关联的程序集[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)或[服务器](../../../analysis-services/scripting/objects/server-element-assl.md)元素  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ClrAssembly>  
      <!-- The following elements extend Assembly -->  
   <Files>...</Files>  
      <PermissionSet>...</PermissionSet>  
</ClrAssembly>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|[程序集](../../../analysis-services/scripting/objects/assembly-element-assl.md)|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无（抽象类型）|  
|子元素|[文件](../../../analysis-services/scripting/collections/files-element-assl.md)， [PermissionSet](../../../analysis-services/scripting/properties/permissionset-element-assl.md)|  
|派生元素|请参阅 [Assembly](../../../analysis-services/scripting/objects/assembly-element-assl.md) （[Database](../../../analysis-services/scripting/collections/assemblies-element-assl.md) 或 [Server](../../../analysis-services/scripting/objects/database-element-assl.md) 的 [Assemblies](../../../analysis-services/scripting/objects/server-element-assl.md)集合）|  
  
## <a name="remarks"></a>注释  
 **ClrAssembly**元素包含需重新创建的文件[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]程序集，关联的实例使用[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]或的实例上的特定数据库[!INCLUDE[ssAS](../../../includes/ssas-md.md)]，以及执行程序集所需的权限。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ClrAssembly>。  
  
## <a name="see-also"></a>另请参阅  
 [文件元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/file-element-assl.md)   
 [ClrAssemblyFile 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)   
 [数据元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/data-element-assl.md)   
 [DataBlock 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/datablock-data-type-assl.md)   
 [块元素 & #40;ASSL & #41;](../../../analysis-services/scripting/collections/blocks-element-assl.md)   
 [块元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/block-element-assl.md)   
 [ComAssembly 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
