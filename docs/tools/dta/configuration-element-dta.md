---
title: 配置元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Configuration element
ms.assetid: 1478e56f-57c4-4441-bac9-1ac91453839b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9a0e0bbcc65dd3b9cb1d6fd53f3d296f995f0527
ms.sourcegitcommit: 0f7cf9b7ab23df15624d27c129ab3a539e8b6457
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2018
ms.locfileid: "51291313"
---
# <a name="configuration-element-dta"></a>配置元素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  指定一个用户指定的配置（由现有和假想的物理设计结构组成），以便数据库引擎优化顾问在优化工作负荷时进行分析。  
  
## <a name="syntax"></a>语法  
  
```  
  
<DTAInput>  
    <Server>...</Server>  
    <Workload>...</Workload>  
    <TuningOptions>...</TuningOptions  
    <Configuration [SpecificationMode="Relative" | "Absolute"]>  
    ...code removed here...  
    </Configuration>  
</DTAInput>  
```  
  
## <a name="element-attributes"></a>元素属性  
  
|配置属性|描述|  
|-----------------------------|-----------------|  
|**SpecificationMode**|可选。 指定数据库引擎优化顾问是依据当前的现有配置分析指定的配置，还是将指定的配置作为一个全新的独立配置进行分析。 使用 string 数据类型将此属性指定为以下允许  值之一：<br /><br /> **相对**：<br />                  依据被优化的数据库中的物理设计结构（索引、索引视图和分区）的当前现有配置来评估指定的配置。 例如：<br /><br /> `<Configuration SpecificationMode="Relative">`<br /><br /> **绝对**：<br />                  将指定配置作为独立配置进行评估。 如果指定 Absolute，则数据库引擎优化顾问将不考虑现有配置。 例如：<br /><br /> `<Configuration SpecificationMode="Absolute">`|  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|描述|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|可选。 对于每个 **DTAInput** 元素可以使用一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[DTAInput 元素 (DTA)](../../tools/dta/dtainput-element-dta.md)|  
|**子元素**|[用于配置的服务器元素 (DTA)](../../tools/dta/server-element-for-configuration-dta.md)|  
  
## <a name="example"></a>示例  
 有关此元素的用法示例，请参阅[用户指定配置 (DTA) 的 XML 输入文件示例](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
