---
title: ParameterDirectionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ParameterDirectionEnum
helpviewer_keywords:
- ParameterDirectionEnum enumeration [ADO]
ms.assetid: c66aa6e6-d4f0-4f0f-9640-e08ae6cfdef3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 68aaa0bfb8aa72c9e94a8b5db65768fe85895f0e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917743"
---
# <a name="parameterdirectionenum"></a>ParameterDirectionEnum
指定是否[参数](../../../ado/reference/ado-api/parameter-object.md)表示输入的参数、 输出参数，这既是输入和输出参数或从存储过程的返回值。  
  
|常量|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adParamInput**|1|默认值。 指示该参数表示的输入的参数。|  
|**adParamInputOutput**|3|指示该参数表示这两个输入和输出参数。|  
|**adParamOutput**|2|指示该参数表示输出参数。|  
|**adParamReturnValue**|4|指示该参数表示返回值。|  
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
