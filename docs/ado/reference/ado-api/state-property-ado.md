---
title: State 属性 (ADO) |Microsoft 文档
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
- Command25::State
helpviewer_keywords:
- State property [ADO]
ms.assetid: 0b993bac-2653-40b1-bcbb-5b57b6aae2bf
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b4e254a4d13f4a210c174e3ef5b8181dd24cefd7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="state-property-ado"></a>State 属性 (ADO)
对象的状态是打开还是已关闭，则指示为所有适用的对象。 如果该对象正在执行的异步方法，指示是连接、 执行，还是检索对象的当前状态。  
  
## <a name="return-value"></a>返回值  
 返回**长**值可以是[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)值。 默认值是**adStateClosed**。  
  
## <a name="remarks"></a>注释  
 你可以使用**状态**属性来随时确定给定对象的当前状态。  
  
 对象的**状态**属性可以具有值的组合。 例如，如果执行语句时，此属性将具有的合并的值**adStateOpen**和**adStateExecuting**。  
  
 **状态**属性是只读的。  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>另请参阅  
 [ConnectionString、 ConnectionTimeout，以及状态属性示例 (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、 ConnectionTimeout 和状态属性示例 （VC + +）](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
