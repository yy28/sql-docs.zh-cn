---
title: 数据源元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8aa0828a58e5b30776f3c856a68873ab8be893f2
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="datasource-element-xmla"></a>DataSource 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含父级的外部数据源绑定[批处理](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)或[过程](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Batch> <!-- or Process>  
...  
   <DataSource>  
      <DatabaseID>...</DatabaseID>  
      <DataSourceID>...</DataSourceID>  
   </DataSource>  
...  
</Batch>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[批处理](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)，[过程](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|子元素|[DatabaseID](../../../analysis-services/xmla/xml-elements-properties/databaseid-element-xmla.md)， [DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 **数据源**元素表示的外部绑定到数据源，使用**批处理**或**过程**命令以临时替代的数据源绑定[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]命令处理的对象。  
  
 有关扩展的行绑定的详细信息，请参阅[数据源和绑定 & #40;SSAS 多维 & #41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
