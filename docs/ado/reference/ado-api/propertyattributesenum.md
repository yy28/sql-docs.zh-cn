---
title: PropertyAttributesEnum |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PropertyAttributesEnum
helpviewer_keywords:
- PropertyAttributesEnum enumeration [ADO]
ms.assetid: 96a01955-a6b4-4cbf-9c73-52bcd1e9fb25
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31260a4336954a2efa0cf001d244b7ad7ff7d6a0
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35280796"
---
# <a name="propertyattributesenum"></a>PropertyAttributesEnum
指定的属性[属性](../../../ado/reference/ado-api/property-object-ado.md)对象。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adPropNotSupported**|0|指示提供程序不支持该属性。|  
|**adPropRequired**|@shouldalert|指示数据源初始化之前，用户必须指定此属性的值。|  
|**adPropOptional**|2|指示用户不必指定此属性的值之前初始化的数据源。|  
|**adPropRead**|512|指示用户可以读取该属性。|  
|**adPropWrite**|1024|指示用户可以设置此属性。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.PropertyAttributes.NOTSUPPORTED|  
|AdoEnums.PropertyAttributes.REQUIRED|  
|AdoEnums.PropertyAttributes.OPTIONAL|  
|AdoEnums.PropertyAttributes.READ|  
|AdoEnums.PropertyAttributes.WRITE|  
  
## <a name="applies-to"></a>适用范围  
 [Attributes 属性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
