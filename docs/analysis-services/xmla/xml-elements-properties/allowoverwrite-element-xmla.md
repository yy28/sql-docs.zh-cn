---
title: AllowOverwrite 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1350d7fba1800f2ec0ea38a6ed57b776e163919a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="allowoverwrite-element-xmla"></a>AllowOverwrite 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  确定是否父[备份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)或[还原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)命令尝试覆盖目标文件或数据库。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <AllowOverwrite>...</AllowOverwrite>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|False|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[备份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)，[还原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 有关**备份**命令， **AllowOverwrite**元素确定该命令是否可以覆盖备份文件中指定**文件**元素。  
  
 有关**还原**元素， **AllowOverwrite**元素确定是否可以覆盖该命令[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中指定数据库**DatabaseName**元素。  
  
## <a name="see-also"></a>另请参阅  
 [DatabaseName 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/databasename-element-xmla.md)   
 [文件元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md)   
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
