---
title: State 属性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command25::State
helpviewer_keywords:
- State property [ADO]
ms.assetid: 0b993bac-2653-40b1-bcbb-5b57b6aae2bf
author: rothja
ms.author: jroth
ms.openlocfilehash: f4fa19bf21764437d3713c434e288b3bb3a3d25d
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242567"
---
# <a name="state-property-ado"></a>State 属性 (ADO)
指示对象的状态是打开还是关闭的所有适用对象。 如果对象正在执行异步方法，则指示对象的当前状态是 "正在连接"、"正在执行" 还是 "正在检索"。  
  
## <a name="return-value"></a>返回值  
 返回一个可以为[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)值的**Long**值。 默认值为**adStateClosed**。  
  
## <a name="remarks"></a>备注  
 你可以随时使用**State**属性来确定给定对象的当前状态。  
  
 对象的**State**属性可以包含值的组合。 例如，如果正在执行某个语句，则此属性将具有**adStateOpen**和**adStateExecuting**的组合值。  
  
 **状态**属性是只读的。  
  
## <a name="applies-to"></a>适用于  

:::row:::
    :::column:::
        [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
        [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
        [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
    :::column-end:::
    :::column:::
        [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另请参阅  
 [ConnectionString、ConnectionTimeout 和 State 属性示例（VB）](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、ConnectionTimeout 和 State 属性示例（VC + +）](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
