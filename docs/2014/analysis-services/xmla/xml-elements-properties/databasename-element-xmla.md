---
title: DatabaseName 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DatabaseName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.databasename
- http://schemas.microsoft.com/analysisservices/2003/engine#DatabaseName
- urn:schemas-microsoft-com:xml-analysis#DatabaseName
helpviewer_keywords:
- DatabaseName element
ms.assetid: 5cfd9a1f-da53-497a-b677-c51be4641bd0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c4727f3554b654687484e6bd273a0d88e557215e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48172677"
---
# <a name="databasename-element-xmla"></a>DatabaseName 元素 (XMLA)
  标识[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]还原父数据库[还原](../xml-elements-commands/restore-element-xmla.md)命令。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Restore>  
   ...  
   <DatabaseName>...</DatabaseName>  
   ...  
</Restore>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[还原](../xml-elements-commands/restore-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `DatabaseName` 元素标识 `Restore` 命令要将备份文件还原到的数据库。 如果此元素未指定或包含空字符串，则使用备份文件中包含的数据库名称。  
  
 如果目标实例中已存在该数据库，除非将父 `AllowOverwrite` 命令的 `Restore` 元素设置为 `True`，否则将发生错误。  
  
## <a name="see-also"></a>请参阅  
 [AllowOverwrite 元素&#40;XMLA&#41;](allowoverwrite-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
