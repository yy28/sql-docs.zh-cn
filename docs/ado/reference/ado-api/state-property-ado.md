---
description: State 属性 (ADO)
title: ) ADO (状态属性 |Microsoft Docs
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
ms.openlocfilehash: 14e9a083c9f80d2c6485a9444211a2796b7fabee
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777346"
---
# <a name="state-property-ado"></a>State 属性 (ADO)
指示对象的状态是打开还是关闭的所有适用对象。 如果对象正在执行异步方法，则指示对象的当前状态是 "正在连接"、"正在执行" 还是 "正在检索"。  
  
## <a name="return-value"></a>返回值  
 返回一个可以为[ObjectStateEnum](./objectstateenum.md)值的**Long**值。 默认值为 **adStateClosed**。  
  
## <a name="remarks"></a>备注  
 你可以随时使用 **State** 属性来确定给定对象的当前状态。  
  
 对象的 **State** 属性可以包含值的组合。 例如，如果正在执行某个语句，则此属性将具有 **adStateOpen** 和 **adStateExecuting**的组合值。  
  
 **状态**属性是只读的。  
  
## <a name="applies-to"></a>适用于  

:::row:::
    :::column:::
        [命令对象 (ADO)](./command-object-ado.md)  
        [连接对象 (ADO)](./connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [记录对象 (ADO)](./record-object-ado.md)  
        [记录集对象 (ADO)](./recordset-object-ado.md)  
    :::column-end:::
    :::column:::
        [流对象 (ADO)](./stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另请参阅  
 [ConnectionString、ConnectionTimeout 和 State 属性示例 (VB) ](./connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、ConnectionTimeout 和 State 属性示例 (VC + +) ](./connectionstring-connectiontimeout-and-state-properties-example-vc.md)