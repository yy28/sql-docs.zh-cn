---
title: "ColumnBinding 数据类型 (ASSL) |Microsoft 文档"
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
apiname: ColumnBinding Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ColumnBinding
helpviewer_keywords: ColumnBinding data type
ms.assetid: 3ab1bac1-6716-4b17-a107-d5f9c744c5e6
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 86d1f2ee2a1e389cc6d6d8a55b59815cc7546d06
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="columnbinding-data-type-assl"></a>ColumnBinding 数据类型 (ASSL)
  定义一个派生的数据类型，表示到数据源视图中的列的绑定[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ColumnBinding>  
   <!-- The following elements extend Binding -->  
   <TableID>...</TableID>  
      <ColumnID>...</ColumnID>  
</ColumnBinding>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|[绑定](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[ColumnID](../../../analysis-services/scripting/properties/columnid-element-eventcolumn-assl.md)， [TableID](../../../analysis-services/scripting/properties/tableid-element-assl.md)|  
|派生元素|请参阅[绑定](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>注释  
 若要创建有效的 XML 元素名称， [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] **数据集**对象编码表名称为它们序列化到 XML 架构定义 (XSD); 例如，名称"Order Details"变为"Order_x0020_Details"。 同样， **ColumnID**和**TableID**中包含元素**ColumnBinding**元素和数据源视图 (DSV) 中的引用对象还必须进行编码在序列化，以确保名称与在 DSV 中的文本直接匹配过程的名称。 Analysis Services 实例将解码这些名称，就像**数据集**对象模型。  
  
 A **TableDefinitions**元素包含的元素使用**TableBinding**数据类型和引用在 DSV 中的表必须还编码名称为它们序列化为 XSD。 但是，表名中**分区**应未编码的绑定，因为这些名称是只需的数据库中存在，并且没有要在 DSV 中表的名称。 不编码表中的名称**分区**绑定还实现以下：  
  
-   使分区的数据定义库 (DDL) 更加简单。  
  
-   提供更高一致性，因为分区即可具有表名称，也可有 SELECT 语句，并且不应对 SELECT 语句进行编码。  
  
 表名和列名不包含分隔符（例如，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的“[”）。  
  
 有关其他信息**绑定**类型，包括表的 Analysis Services 脚本语言 (ASSL) 对象**绑定**类型和继承层次结构的**绑定**类型，请参阅[绑定数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 ASSL 中数据绑定的概述，请参阅[数据源和绑定 &#40;SSAS 多维 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 在 AMO 对象模型中，对应的元素为 <xref:Microsoft.AnalysisServices.ColumnBinding>。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
