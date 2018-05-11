---
title: ApplyCompression 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6b95e6c2a76c6642c032331ca08a46cece1e1287
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="applycompression-element-xmla"></a>ApplyCompression 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  确定是否父[备份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)命令压缩备份文件。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Backup>  
   ...  
   <ApplyCompression>...</ApplyCompression>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|True|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[备份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
