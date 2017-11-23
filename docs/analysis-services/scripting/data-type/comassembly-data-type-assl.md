---
title: "ComAssembly 数据类型 (ASSL) |Microsoft 文档"
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
apiname: ComAssembly Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ComAssembly
helpviewer_keywords: ComAssembly data type
ms.assetid: 23c0f4b3-b6ac-4ec8-9254-74d2f84f5244
caps.latest.revision: "48"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bd2c0101a6dcdc35c2834dddb8df6aa295e2f8d6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="comassembly-data-type-assl"></a>ComAssembly 数据类型 (ASSL)
  定义一个派生的数据类型，表示与关联的 COM 库[服务器](../../../analysis-services/scripting/objects/server-element-assl.md)或[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。  
  
> [!IMPORTANT]  
>  COM 程序集可能会造成安全风险。 由于此风险和其他注意事项， [!INCLUDE[ssASversion10](../../../includes/ssasversion10-md.md)]中不推荐使用 COM 程序集。 未来版本可能不支持 COM 程序集。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ComAssembly>  
      <!-- The following elements extend Assembly -->  
   <Source>...</Source>  
</ComAssembly>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|[程序集](../../../analysis-services/scripting/objects/assembly-element-assl.md)|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[数据源](../../../analysis-services/scripting/properties/source-element-comassembly-assl.md)|  
|派生元素|请参阅[程序集](../../../analysis-services/scripting/objects/assembly-element-assl.md)([程序集](../../../analysis-services/scripting/collections/assemblies-element-assl.md)集合[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)或[服务器](../../../analysis-services/scripting/objects/server-element-assl.md))|  
  
## <a name="remarks"></a>注释  
 **ComAssembly**元素包含与实例关联的 COM 库 （完全限定的文件名或的编程标识符） 的引用[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]或具有特定实例上的数据库[!INCLUDE[ssAS](../../../includes/ssas-md.md)]。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ComAssembly>。  
  
## <a name="see-also"></a>另请参阅  
 [ClrAssembly 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
