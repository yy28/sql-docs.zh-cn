---
title: ClrAssembly 数据类型 (ASSL) |Microsoft Docs
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
- ClrAssembly Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ClrAssembly
helpviewer_keywords:
- ClrAssembly data type
ms.assetid: 3f5dc5a1-ebd6-41b8-ac04-91d4de137eb4
caps.latest.revision: 44
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 63809f3dd903878baf5eabf1642430fbe0d9aa8e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37235577"
---
# <a name="clrassembly-data-type-assl"></a>ClrAssembly 数据类型 (ASSL)
  定义一个派生的数据类型，表示[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]程序集与关联[数据库](../objects/database-element-assl.md)或[Server](../objects/server-element-assl.md)元素  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ClrAssembly>  
      <!-- The following elements extend Assembly -->  
   <Files>...</Files>  
      <PermissionSet>...</PermissionSet>  
</ClrAssembly>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|[程序集](../objects/assembly-element-assl.md)|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无（抽象类型）|  
|子元素|[文件](../collections/files-element-assl.md)， [PermissionSet](../properties/permissionset-element-assl.md)|  
|派生元素|请参阅[程序集](../objects/assembly-element-assl.md)([程序集](../collections/assemblies-element-assl.md)的集合[数据库](../objects/database-element-assl.md)或者[Server](../objects/server-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 `ClrAssembly`元素包含重新创建所需的文件[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]程序集，关联的实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]或与特定数据库的实例上[!INCLUDE[ssAS](../../../includes/ssas-md.md)]，并将若要执行该程序集所需的权限。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ClrAssembly>。  
  
## <a name="see-also"></a>请参阅  
 [文件元素&#40;ASSL&#41;](../objects/file-element-assl.md)   
 [ClrAssemblyFile 数据类型&#40;ASSL&#41;](clrassemblyfile-data-type-assl.md)   
 [数据元素&#40;ASSL&#41;](../objects/data-element-assl.md)   
 [DataBlock 数据类型&#40;ASSL&#41;](datablock-data-type-assl.md)   
 [阻止元素&#40;ASSL&#41;](../collections/blocks-element-assl.md)   
 [Block 元素&#40;ASSL&#41;](../objects/block-element-assl.md)   
 [ComAssembly 数据类型&#40;ASSL&#41;](assembly-data-type-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
