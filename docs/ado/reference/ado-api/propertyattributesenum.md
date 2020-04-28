---
title: PropertyAttributesEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PropertyAttributesEnum
helpviewer_keywords:
- PropertyAttributesEnum enumeration [ADO]
ms.assetid: 96a01955-a6b4-4cbf-9c73-52bcd1e9fb25
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 624fa1976792a700342a114f82aa5ca6b75c70ea
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931560"
---
# <a name="propertyattributesenum"></a>PropertyAttributesEnum
指定[属性](../../../ado/reference/ado-api/property-object-ado.md)对象的特性。  
  
|Constant|值|说明|  
|--------------|-----------|-----------------|  
|**adPropNotSupported**|0|指示该提供程序不支持该属性。|  
|**adPropRequired**|1|指示在初始化数据源之前，用户必须为此属性指定一个值。|  
|**adPropOptional**|2|指示在初始化数据源之前，用户无需指定此属性的值。|  
|**adPropRead**|512|指示用户可以读取属性。|  
|**adPropWrite**|1024|指示用户可以设置属性。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|Constant|  
|--------------|  
|AdoEnums. PropertyAttributes. NOTSUPPORTED|  
|AdoEnums. PropertyAttributes. 必需|  
|AdoEnums. PropertyAttributes。可选|  
|AdoEnums. PropertyAttributes. READ|  
|AdoEnums. PropertyAttributes|  
  
## <a name="applies-to"></a>应用于  
 [Attributes 属性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
