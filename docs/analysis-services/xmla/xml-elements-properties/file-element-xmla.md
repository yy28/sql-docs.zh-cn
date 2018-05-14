---
title: 文件元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1d7422a79112ef09da406eccf6f52f5b71851607
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="file-element-xmla"></a>File 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  标识要使用由容器的父文件[备份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)或[还原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)命令，或通过父[位置](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)元素。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Backup> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <File>...</File>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[备份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)，[位置](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)，[还原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **文件**元素包含一个 UNC 文件名称、 和父元素确定使用**文件**元素。  
  
 有关**备份**命令，**文件**元素确定创建的备份文件的名称**备份**命令。 如果路径未指定的文件名称的一部分，在指定的路径**BackupDir**的实例的配置属性[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]使用。 如果指定的文件已存在，除非发生错误**AllowOverwrite**元素的父**备份**命令设置为**True**。  
  
 有关**还原**命令，**文件**元素确定要还原的备份文件的名称**还原**命令。  
  
 有关**位置**元素，**文件**元素描述的远程备份文件[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]包含远程分区的实例。 有关备份和还原远程分区的详细信息，请参阅[Backing Up，正在还原，和同步数据库 & #40;XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>另请参阅  
 [AllowOverwrite 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md)   
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
