---
title: State 属性 (ADO MD) |Microsoft 文档
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
- State
- Cellset::State
helpviewer_keywords:
- State property [ADO MD]
ms.assetid: 06d480ca-9eb6-4570-a45d-a73539bddd32
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8541ca4202fcf6f0f450ab38e2ea74b609b529c3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="state-property-ado-md"></a>State 属性 (ADO MD)
指示单元集的当前状态。  
  
## <a name="return-values"></a>返回值  
 返回**长**整数，指示的当前状态[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象，并是只读的。 以下为有效值： **adStateClosed** (0) 和**adStateOpen** (1)。  
  
## <a name="remarks"></a>注释  
 若要使用[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)常量名，必须在你的项目中引用的 ADO 类型库。 请参阅[利用 ADO MD 使用 ADO](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)有关详细信息。  
  
## <a name="applies-to"></a>适用范围  
 [单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [Close 方法 (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Open 方法 (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
