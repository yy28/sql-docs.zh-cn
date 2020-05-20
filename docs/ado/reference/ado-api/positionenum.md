---
title: PositionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PositionEnum
helpviewer_keywords:
- PositionEnum enumeration
ms.assetid: e69af0a5-3405-4b72-9c6e-6b188ff746fd
author: rothja
ms.author: jroth
ms.openlocfilehash: 57a440a97dcdf1c0fddcff8017e0c2d04967b92d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763338"
---
# <a name="positionenum"></a>PositionEnum
指定记录指针在[记录集中](../../../ado/reference/ado-api/recordset-object-ado.md)的当前位置。  
  
|返回的常量|值|说明|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|指示当前记录指针处于 BOF （即[bof](../../../ado/reference/ado-api/bof-eof-properties-ado.md)属性为**True**）。|  
|**adPosEOF**|-3|指示当前记录指针位于 EOF （即[eof](../../../ado/reference/ado-api/bof-eof-properties-ado.md)属性为**True**）。|  
|**adPosUnknown**|-1|指示**记录集**为空，当前位置未知，或者提供程序不支持[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)或[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)属性。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums。未知|  
  
## <a name="applies-to"></a>应用于  
  
|||  
|-|-|  
|[AbsolutePage 属性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)|[AbsolutePosition 属性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|
