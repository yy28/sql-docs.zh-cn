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
author: rothja
ms.author: jroth
ms.openlocfilehash: b6b8c5c9a593177155f2f22d7dba4e38515e0dce
ms.sourcegitcommit: 4b775a3ce453b757c7435cc2a4c9b35d0c5a8a9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2020
ms.locfileid: "87472603"
---
# <a name="objectstateenum"></a>ObjectStateEnum
指定对象是打开还是关闭，连接到数据源，执行命令，或检索数据。  
  
|返回的常量|值|描述|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|指示对象已关闭。|  
|**adStateOpen**|1|指示对象已打开。|  
|**adStateConnecting**|2|指示对象正在连接。|  
|**adStateExecuting**|4|指示对象正在执行命令。|  
|**adStateFetching**|8|指示正在检索对象的行。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums.ObjectState.CLOSED|  
|AdoEnums.ObjectState.OPEN|  
|AdoEnums.ObjectState.CONNECTING|  
|AdoEnums.ObjectState.EXECUTING|  
|AdoEnums.ObjectState.FETCHING|  
  
## <a name="applies-to"></a>适用于  

:::row:::
    :::column:::
        [State 属性 (ADO)](../../../ado/reference/ado-api/state-property-ado.md)  
    :::column-end:::
    :::column:::
        [State 属性 (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)  
    :::column-end:::
:::row-end:::
