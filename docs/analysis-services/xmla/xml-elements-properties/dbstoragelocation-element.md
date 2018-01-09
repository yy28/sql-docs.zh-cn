---
title: "DbStorageLocation 元素 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DbStorageLocation element
ms.assetid: 1f448249-103a-479f-ae86-b0017acd0436
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bf2bc5ab8c0419260049d8e588fd491a50099135
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="dbstoragelocation-element"></a>DbStorageLocation 元素
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]指定的文件夹位置[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]创建和管理所有数据库数据和元数据文件。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Database>  
...  
   <ddl100_100:DbStorageLocation>...</ddl100_100:DbStorageLocation>  
...  
</Database>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|“”|  
|基数|0-1：只能出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[“数据库”](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 必须将 **DbStorageLocation** 数据库属性设置为现有 UNC 文件夹路径或空字符串。 空字符串是服务器数据文件夹的默认值。 如果该文件夹不存在，则在执行 **Create**、 **Attach**、或 **Alter** 命令时会引发错误。  
  
 另外，不能将 **DbStorageLocation** 数据库属性设置为指向服务器数据文件夹或其任何子文件夹之一。 如果该位置指向服务器数据文件夹或其任何子文件夹之一，则在执行 **Create**、 **Attach**、或 **Alter** 命令时会引发错误。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [附加和分离 Analysis Services 数据库](../../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  
