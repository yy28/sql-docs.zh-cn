---
title: 执行方法 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 019ac154ef902009405f11bcc7023ea831d1f71b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="xml-elements---methods---execute"></a>XML 元素的方法的执行
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  将 XML Analysis (XMLA) 命令发送到的实例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 这包括涉及数据传输的请求，如检索或更新服务器上的数据。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-1：出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[命令](../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)，[参数](../../analysis-services/xmla/xml-elements-properties/parameters-element-xmla.md)，[属性](../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 **执行**方法执行 XMLA 命令中提供**命令**元素并返回任何生成的数据使用 XMLA[行集](../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md)（适用于表格结果的数据类型设置） 或 XMLA [MDDataSet](../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)数据类型 （对于多维结果集。）  
  
## <a name="example"></a>示例  
 下面的代码示例演示了**执行**包含多维表达式 (MDX) SELECT 语句的方法调用。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [XML 数据类型 & #40;XMLA & #41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [发现方法&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)   
 [方法&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods.md)   
 [XML 元素 & #40;XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Analysis Services 架构行集](../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
