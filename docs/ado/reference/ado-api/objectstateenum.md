---
title: ObjectStateEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ObjectStateEnum
helpviewer_keywords:
- ObjectStateEnum enumeration [ADO]
ms.assetid: 32746558-097b-4749-989e-519aadf7e3f4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 708d146aaa40d873e0a519c860a047d4b1f93161
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931929"
---
# <a name="objectstateenum"></a>ObjectStateEnum
指定对象是打开还是关闭，连接到数据源，执行命令，或检索数据。  
  
|一直|值|说明|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|指示对象已关闭。|  
|**adStateOpen**|1|指示对象已打开。|  
|**adStateConnecting**|2|指示对象正在连接。|  
|**adStateExecuting**|4|指示对象正在执行命令。|  
|**adStateFetching**|8|指示正在检索对象的行。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|一直|  
|--------------|  
|AdoEnums.ObjectState.CLOSED|  
|AdoEnums.ObjectState.OPEN|  
|AdoEnums.ObjectState.CONNECTING|  
|AdoEnums.ObjectState.EXECUTING|  
|AdoEnums.ObjectState.FETCHING|  
  
## <a name="applies-to"></a>应用于  
  
|||  
|-|-|  
|[State 属性 (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)|[State 属性 (ADO)](../../../ado/reference/ado-api/state-property-ado.md)|
