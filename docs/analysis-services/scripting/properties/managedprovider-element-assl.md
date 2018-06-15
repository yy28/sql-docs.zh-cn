---
title: ManagedProvider 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 627c57974a5d42c4be3e4fb54d828e47c45ca97f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34034388"
---
# <a name="managedprovider-element-assl"></a>ManagedProvider 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含派生自元素所使用的托管提供程序的名称[数据源](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)数据类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataSource>  
   ...  
   <ManagedProvider>...</ManagedProvider>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 如果数据源使用托管提供程序， **ManagedProvider**元素包含托管提供程序的名称。  
  
## <a name="see-also"></a>另请参阅  
 [命名元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/name-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
