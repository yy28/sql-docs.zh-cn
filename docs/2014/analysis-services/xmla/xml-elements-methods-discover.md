---
title: Discover 方法 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Discover Method
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#
- http://schemas.microsoft.com/analysisservices/2003/engine#
- microsoft.xml.analysis.discover
- urn:schemas-microsoft-com:xml-analysis#Discover
- Discover
helpviewer_keywords:
- Discover method
ms.assetid: 0eb52d88-c081-416e-a229-610e4373b0b3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 91ea30a495eb76c22075007f48e3ae721504ef49
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48116317"
---
# <a name="discover-method-xmla"></a>Discover 方法 (XMLA)
  实例中检索信息，如可用数据库或针对特定对象的详细信息的列表[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 使用 `Discover` 方法检索到的数据取决于传递给该方法的参数的值。  
  
 **Namespace** urn： 架构-microsoft-com:xml-分析  
  
 **SOAP 操作**"urn： 架构-microsoft-com:xml-分析： 发现"  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Discover>  
   <RequestType>...</RequestType>  
   <Restrictions>...</Restrictions>  
   <Properties>...</Properties>  
</Discover>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[属性](xml-elements-properties/properties-element-xmla.md)， [RequestType](xml-elements-properties/type-element-xmla.md)，[限制](xml-elements-properties/restrictions-element-xmla.md)|  
  
## <a name="remarks"></a>备注  
 `Discover` 方法请求有关 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例和对象的元数据。 使用 XMLA 返回元数据[行集](xml-data-types/rowset-data-type-xmla.md)数据类型。  
  
## <a name="example"></a>示例  
 在以下代码示例中，客户端发送 `Discover` 调用以从 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 示例 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库请求多维数据集列表：  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <RequestType>MDSCHEMA_CUBES</RequestType>  
   <Restrictions>  
      <RestrictionList>  
         <CATALOG_NAME>Adventure Works DW Multidimensional 2012</CATALOG_NAME>  
      </RestrictionList>  
   </Restrictions>  
   <Properties>  
      <PropertyList>  
         <DataSourceInfo>Provider=MSOLAP;Data Source=local;</DataSourceInfo>  
         <Catalog>Adventure Works DW Multidimensional 2012</Catalog>  
         <Format>Tabular</Format>  
      </PropertyList>  
   </Properties>  
</Discover>  
```  
  
## <a name="see-also"></a>请参阅  
 [XML 数据类型&#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)   
 [执行方法&#40;XMLA&#41;](xml-elements-methods-execute.md)   
 [方法&#40;XMLA&#41;](xml-elements-methods.md)   
 [XML 元素&#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [Analysis Services 架构行集](../schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
