---
title: ClrAssembly 数据类型 (ASSL) |Microsoft 文档
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
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e17992a5d15113ec0de5dd75978f932cb83d11c8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024919"
---
# <a name="clrassembly-data-type-assl"></a>ClrAssembly 数据类型 (ASSL)
  定义一个派生的数据类型，表示[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]与关联的程序集[数据库](../objects/database-element-assl.md)或[服务器](../objects/server-element-assl.md)元素  
  
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
|派生元素|请参阅[程序集](../objects/assembly-element-assl.md)([程序集](../collections/assemblies-element-assl.md)集合[数据库](../objects/database-element-assl.md)或[服务器](../objects/server-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 `ClrAssembly`元素包含需重新创建的文件[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]程序集，关联的实例使用[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]或使用的实例上的特定数据库[!INCLUDE[ssAS](../../../includes/ssas-md.md)]，以及若要执行程序集而需要的权限。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ClrAssembly>。  
  
## <a name="see-also"></a>请参阅  
 [文件元素&#40;ASSL&#41;](../objects/file-element-assl.md)   
 [ClrAssemblyFile 数据类型&#40;ASSL&#41;](clrassemblyfile-data-type-assl.md)   
 [数据元素&#40;ASSL&#41;](../objects/data-element-assl.md)   
 [DataBlock 数据类型&#40;ASSL&#41;](datablock-data-type-assl.md)   
 [阻止元素&#40;ASSL&#41;](../collections/blocks-element-assl.md)   
 [阻止元素&#40;ASSL&#41;](../objects/block-element-assl.md)   
 [ComAssembly 数据类型&#40;ASSL&#41;](assembly-data-type-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  