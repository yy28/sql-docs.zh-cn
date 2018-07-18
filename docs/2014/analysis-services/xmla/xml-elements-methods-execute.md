---
title: Execute 方法 (XMLA) |Microsoft Docs
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
- Execute Method
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- EXECUTE
- urn:schemas-microsoft-com:xml-analysis#
- http://schemas.microsoft.com/analysisservices/2003/engine#
- microsoft.xml.analysis.execute
- urn:schemas-microsoft-com:xml-analysis#Execute
helpviewer_keywords:
- Execute method
ms.assetid: 0fff5221-7164-4bbc-ab58-49cf04c52664
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ec3fa458148638af5431b4a519acf8556d29b122
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37235557"
---
# <a name="execute-method-xmla"></a>Execute 方法 (XMLA)
  将 XML for Analysis (XMLA) 命令发送到的实例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 这包括涉及数据传输的请求，如检索或更新服务器上的数据。  
  
 **Namespace** urn： 架构-microsoft-com:xml-分析  
  
 **SOAP 操作**"urn： 架构-microsoft-com:xml-分析： 执行"  
  
## <a name="syntax"></a>语法  
  
```  
  
<Execute>  
   <Command>...</Command>  
   <Properties>...</Properties>  
   <Parameters>...</Parameters>  
</Execute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[命令](xml-elements-properties/command-element-xmla.md)，[参数](xml-elements-properties/parameters-element-xmla.md)，[属性](xml-elements-properties/properties-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Execute`方法执行 XMLA 命令中提供`Command`元素，并返回任何生成的数据使用 XMLA[行集](xml-data-types/rowset-data-type-xmla.md)数据类型 （适用于表格结果集） 或 XMLA [MDDataSet](xml-data-types/mddataset-data-type-xmla.md)数据类型 （用于多维结果集。）  
  
## <a name="example"></a>示例  
 下面的代码示例是一个包含多维表达式 (MDX) SELECT 语句的 `Execute` 方法调用的示例。  
  
```  
<Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <Command>  
      <Statement>  
         SELECT [Measures].MEMBERS ON COLUMNS FROM [Adventure Works]  
      </Statement>  
   </Command>  
   <Properties>  
      <PropertyList>  
         <DataSourceInfo>Provider=MSOLAP;Data Source=local;</DataSourceInfo>  
         <Catalog>Adventure Works DW Multidimensional 2012</Catalog>  
         <Format>Multidimensional</Format>  
         <AxisFormat>ClusterFormat</AxisFormat>  
      </PropertyList>  
   </Properties>  
</Execute>  
```  
  
## <a name="see-also"></a>请参阅  
 [XML 数据类型&#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)   
 [发现方法&#40;XMLA&#41;](xml-elements-methods-discover.md)   
 [方法&#40;XMLA&#41;](xml-elements-methods.md)   
 [XML 元素&#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [Analysis Services 架构行集](../schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
