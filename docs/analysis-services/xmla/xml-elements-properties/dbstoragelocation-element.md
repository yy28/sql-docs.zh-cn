---
title: "DbStorageLocation 元素 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DbStorageLocation element
ms.assetid: 1f448249-103a-479f-ae86-b0017acd0436
caps.latest.revision: 15
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9267f5858eb837efdbcd84fb040934e767835d4f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dbstoragelocation-element"></a>DbStorageLocation 元素
  指定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 在其中创建和管理所有数据库数据和元数据文件的文件夹。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Database>  
...  
   <ddl100_100:DbStorageLocation>...</ddl100_100:DbStorageLocation>  
...  
</Database>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|“”|  
|基数|0-1：只能出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[数据库](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 必须将 **DbStorageLocation** 数据库属性设置为现有 UNC 文件夹路径或空字符串。 空字符串是服务器数据文件夹的默认值。 如果该文件夹不存在，则在执行 **Create**、 **Attach**、或 **Alter** 命令时会引发错误。  
  
 另外，不能将 **DbStorageLocation** 数据库属性设置为指向服务器数据文件夹或其任何子文件夹之一。 如果该位置指向服务器数据文件夹或其任何子文件夹之一，则在执行 **Create**、 **Attach**、或 **Alter** 命令时会引发错误。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [附加和分离 Analysis Services 数据库](../../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  

