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
manager: craigg
ms.openlocfilehash: 560e95bdafe3f5bbae82b200d8f7db0dcb121911
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713735"
---
# <a name="objectstateenum"></a>ObjectStateEnum
指定对象是否为开放还是闭合，连接到数据源，执行命令，或检索数据。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|指示对象已关闭。|  
|**adStateOpen**|1|指示对象处于打开状态。|  
|**adStateConnecting**|2|指示连接对象。|  
|**adStateExecuting**|4|指示该对象正在执行命令。|  
|**adStateFetching**|8|指示正在检索对象的行。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.ObjectState.CLOSED|  
|AdoEnums.ObjectState.OPEN|  
|AdoEnums.ObjectState.CONNECTING|  
|AdoEnums.ObjectState.EXECUTING|  
|AdoEnums.ObjectState.FETCHING|  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[State 属性 (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)|[State 属性 (ADO)](../../../ado/reference/ado-api/state-property-ado.md)|
