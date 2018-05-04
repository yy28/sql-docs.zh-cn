---
title: ParameterDirectionEnum |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ParameterDirectionEnum
helpviewer_keywords:
- ParameterDirectionEnum enumeration [ADO]
ms.assetid: c66aa6e6-d4f0-4f0f-9640-e08ae6cfdef3
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd6f885b4e69ce73262961cf545eed2fa5a1c4da
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="parameterdirectionenum"></a>ParameterDirectionEnum
指定是否[参数](../../../ado/reference/ado-api/parameter-object.md)表示输入的参数、 输出参数，这两个输入和输出参数或存储过程的返回值。  
  
|常量|“值”|Description|  
|--------------|-----------|-----------------|  
|**adParamInput**|1|默认值。 指示该参数表示输入的参数。|  
|**adParamInputOutput**|3|指示该参数表示一个输入和输出参数。|  
|**adParamOutput**|2|指示该参数表示输出参数。|  
|**adParamReturnValue**|4|指示该参数表示的返回值。|  
|**adParamUnknown**|0|指示参数方向为未知。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.ParameterDirection.INPUT|  
|AdoEnums.ParameterDirection.INPUTOUTPUT|  
|AdoEnums.ParameterDirection.OUTPUT|  
|AdoEnums.ParameterDirection.RETURNVALUE|  
|AdoEnums.ParameterDirection.UNKNOWN|  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[CreateParameter 方法 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)|[Direction 属性](../../../ado/reference/ado-api/direction-property.md)|
