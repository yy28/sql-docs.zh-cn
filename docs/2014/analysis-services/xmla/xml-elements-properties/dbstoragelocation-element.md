---
title: DbStorageLocation 元素 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- DbStorageLocation element
ms.assetid: 1f448249-103a-479f-ae86-b0017acd0436
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cdee1fc2d62f63eb70e5aecd47c32693a9fbd155
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48173917"
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
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `DbStorageLocation`数据库属性必须设置为现有 UNC 文件夹路径或空字符串。 空字符串是服务器数据文件夹的默认值。 如果该文件夹不存在，则在执行 `Create`、`Attach`、或 `Alter` 命令时会引发错误。  
  
 此外，`DbStorageLocation`数据库属性不能设置为指向服务器数据文件夹或任何子文件夹。 如果该位置指向服务器数据文件夹或其任何子文件夹之一，则在执行 `Create`、`Attach`、或 `Alter` 命令时会引发错误。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [附加和分离 Analysis Services 数据库](../../multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  
