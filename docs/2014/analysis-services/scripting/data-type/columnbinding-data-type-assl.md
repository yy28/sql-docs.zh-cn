---
title: ColumnBinding 数据类型 (ASSL) |Microsoft Docs
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
- ColumnBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ColumnBinding
helpviewer_keywords:
- ColumnBinding data type
ms.assetid: 3ab1bac1-6716-4b17-a107-d5f9c744c5e6
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 227801af8b66d66ebeba50d2713267720adffa9a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200107"
---
# <a name="columnbinding-data-type-assl"></a>ColumnBinding 数据类型 (ASSL)
  定义一个派生的数据类型，表示绑定到数据源视图中的列[DataItem](dataitem-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ColumnBinding>  
   <!-- The following elements extend Binding -->  
   <TableID>...</TableID>  
      <ColumnID>...</ColumnID>  
</ColumnBinding>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|[绑定](binding-data-type-assl.md)|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[ColumnID](../properties/columnid-element-eventcolumn-assl.md)， [TableID](../properties/id-element-assl.md)|  
|派生元素|请参阅[绑定](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 若要创建有效的 XML 元素名称， [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] `DataSet`对象对表名称进行编码，因为它们序列化到 XML 架构定义 (XSD); 例如，名称"Order Details"变为"Order_x0020_Details"。 同样，在序列化过程中，`ColumnID` 元素中包含的、引用数据源视图 (DSV) 中对象的 `TableID` 和 `ColumnBinding` 元素也必须对名称进行编码，以确保名称与 DSV 中的文本直接匹配。 正如 `DataSet` 对象模型一样，Analysis Services 实例会对这些名称进行解码。  
  
 包含在使用 `TableDefinitions` 数据类型的元素中并引用 DSV 中的表的 `TableBinding` 元素也必须在名称序列化为 XSD 时对它们进行编码。 但不应对 `Partition` 绑定中的表名称进行编码，因为这些名称只是存在于数据库中的表的名称，不必存储在 DSV 中。 不对 `Partition` 绑定中的表名称进行编码还可带来以下好处：  
  
-   使分区的数据定义库 (DDL) 更加简单。  
  
-   提供更高一致性，因为分区即可具有表名称，也可有 SELECT 语句，并且不应对 SELECT 语句进行编码。  
  
 表名和列名不包含分隔符（例如，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的“[”）。  
  
 有关其他信息`Binding`类型，包括 Analysis Services 脚本语言 (ASSL) 对象的表`Binding`类型和继承层次结构`Binding`类型，请参阅[&#40;ASSL&#41;](binding-data-type-assl.md)。  
  
 有关 ASSL 中数据绑定的概述，请参阅[数据源和绑定&#40;SSAS 多维&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
 在 AMO 对象模型中，对应的元素为 <xref:Microsoft.AnalysisServices.ColumnBinding>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
