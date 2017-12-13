---
title: "名称元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Name Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Name
helpviewer_keywords: Name element
ms.assetid: caf2af86-5f9c-4e14-8168-f3a79248b4fe
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 80a083e924e6265689f9852bae46b0c0c184c765
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="name-element-assl"></a>Name 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]包含父元素的名称。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Action> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Name>...</Name>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（最多 100 个字符）|  
|默认值|不定|  
|基数|1-1： 发生一次，并且一次的必需的元素|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[操作](../../../analysis-services/scripting/objects/action-element-assl.md)，[聚合](../../../analysis-services/scripting/objects/aggregation-element-assl.md)， [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)， [AlgorithmParameter](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)，[批注](../../../analysis-services/scripting/objects/annotation-element-assl.md)， [程序集](../../../analysis-services/scripting/objects/assembly-element-assl.md)， [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)，[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)， [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)， [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md)， [数据库](../../../analysis-services/scripting/objects/database-element-assl.md)，[数据源](../../../analysis-services/scripting/objects/datasource-element-assl.md)， [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)，[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)，[组](../../../analysis-services/scripting/objects/group-element-assl.md)，[层次结构](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)， [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)，[级别](../../../analysis-services/scripting/objects/level-element-assl.md)， [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)， [度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)， [MemberProperty](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)， [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)， [MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)， [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)， [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)，[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)，[权限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)， [透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)， [PerspectiveCalculation](../../../analysis-services/scripting/data-type/perspectivecalculation-data-type-assl.md)， [ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md)， [ReportParameter](../../../analysis-services/scripting/objects/reportparameter-element-assl.md)， [角色](../../../analysis-services/scripting/objects/role-element-assl.md)，[服务器](../../../analysis-services/scripting/objects/server-element-assl.md)， [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)，[跟踪](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 每个元素，用于定义对象 (实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，层次结构和属性，等) 具有**名称**作为属性的元素。 值**名称**元素具有以下限制：  
  
-   该值不可包含前导空格或尾随空格。 如果的值中包含前导空格或尾随空格**名称**元素，这些空间会隐式移除[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
-   该值不应包含控制字符。 强烈建议名称中不要出现控制字符，这些字符有时会导致 XML 验证错误。  
  
     使用创建的对象**GetNewName**中的方法[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，AMO 检查并随后删除任何控制字符、 前导空格或尾随空格的名称中。 此原因，使用**GetNewName**是建议的设置对象名称的方法。  
  
     但是，如果你设置**名称**直接属性、 不执行检查，可能会导致 XML 验证错误的相同验证。 实际是否会出现错误取决于名称中出现的是哪种控制字符。  
  
     虽然对象名称中绝对不应该使用控制字符，但 Analysis Services 并未严格阻止它们。 之前版本的 Analysis Services 有时接受对象名称中的控制字符。 此原因，SQL Server 2016 Analysis Services 和更高版本将忽略对象名称以避免破坏较旧的解决方案中的控制字符。  
  
-   不可使用以下保留值：  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   COM1 到 COM9（COM1、COM2、COM3 等）  
  
    -   CON  
  
    -   LPT1 到 LPT9（LPT1、LPT2、LPT3 等）  
  
    -   NUL  
  
    -   PRN  
  
 下表列出的值不能使用的其他字符**名称**元素，具体取决于父元素。  
  
|父元素|无效的字符|  
|--------------------|------------------------|  
|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|此名称必须遵循 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 计算机名称规则。 IP 地址无效。|  
|[数据源](../../../analysis-services/scripting/objects/datasource-element-assl.md)|:/\\*&#124;?"()[]{}<>|  
|[级别](../../../analysis-services/scripting/objects/level-element-assl.md)，[属性元素](../../../analysis-services/scripting/objects/attribute-element-assl.md)|.,;'`:/\\*&#124;?"&%$!+=[]{}<>|  
|所有其他父元素|.,;'`:/\\*&#124;?"&%$!+=()[]{}<>|  
  
## <a name="see-also"></a>另请参阅  
 [ID 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/id-element-assl.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
