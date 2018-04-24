---
title: ObjectStateEnum |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ObjectStateEnum
helpviewer_keywords:
- ObjectStateEnum enumeration [ADO]
ms.assetid: 32746558-097b-4749-989e-519aadf7e3f4
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2027cd4b7f034333d383f570860fddf841097b7d
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="objectstateenum"></a>ObjectStateEnum
指定的对象是否是打开还是关闭，连接到数据源，执行命令，或检索数据。  
  
|常量|“值”|Description|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|指示对象已关闭。|  
|**adStateOpen**|1|指示该对象已打开。|  
|**adStateConnecting**|2|指示连接对象。|  
|**adStateExecuting**|4|指示对象执行命令。|  
|**adStateFetching**|8|指示正在检索的对象的行。|  
  
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
