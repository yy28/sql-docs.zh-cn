---
title: ComAssembly 数据类型 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 409eb7fd0dd093e7bd44a642868c8dd87d25f04e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="comassembly-data-type-assl"></a>ComAssembly 数据类型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义一个派生数据类型，该类型表示与 [Server](../../../analysis-services/scripting/objects/server-element-assl.md) 或 [Database](../../../analysis-services/scripting/objects/database-element-assl.md) 元素关联的 COM 库。  
  
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
|派生元素|请参阅 [Assembly](../../../analysis-services/scripting/objects/assembly-element-assl.md) （[Database](../../../analysis-services/scripting/collections/assemblies-element-assl.md) 或 [Server](../../../analysis-services/scripting/objects/database-element-assl.md) 的 [Assemblies](../../../analysis-services/scripting/objects/server-element-assl.md)集合）|  
  
## <a name="remarks"></a>注释  
 **ComAssembly**元素包含与实例关联的 COM 库 （完全限定的文件名或的编程标识符） 的引用[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]或具有特定实例上的数据库[!INCLUDE[ssAS](../../../includes/ssas-md.md)]。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ComAssembly>。  
  
## <a name="see-also"></a>另请参阅  
 [ClrAssembly 数据类型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
