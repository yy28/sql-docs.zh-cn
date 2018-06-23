---
title: DbStorageLocation 元素 |Microsoft 文档
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
helpviewer_keywords:
- DbStorageLocation element
ms.assetid: 1f448249-103a-479f-ae86-b0017acd0436
caps.latest.revision: 15
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 651dc0424c492efefa7828ae327f9bdcf837ed77
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026402"
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|“”|  
|基数|0-1：只能出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[“数据库”](database-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `DbStorageLocation`数据库属性必须设置为现有 UNC 文件夹路径或空字符串。 空字符串是服务器数据文件夹的默认值。 如果该文件夹不存在，则在执行 `Create`、`Attach`、或 `Alter` 命令时会引发错误。  
  
 此外，`DbStorageLocation`数据库属性不能设置为指向服务器数据文件夹或其任何子文件夹。 如果该位置指向服务器数据文件夹或其任何子文件夹之一，则在执行 `Create`、`Attach`、或 `Alter` 命令时会引发错误。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [附加和分离 Analysis Services 数据库](../../multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  