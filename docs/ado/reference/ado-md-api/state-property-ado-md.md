---
title: State 属性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- State
- Cellset::State
helpviewer_keywords:
- State property [ADO MD]
ms.assetid: 06d480ca-9eb6-4570-a45d-a73539bddd32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 812863395c2980f341ed2419eee1d9d661f19dd0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63308602"
---
# <a name="state-property-ado-md"></a>State 属性 (ADO MD)
指示在单元集中的当前状态。  
  
## <a name="return-values"></a>返回值  
 返回**长**整数，指示当前的条件[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象，并是只读的。 以下列出了有效值： **adStateClosed** (0) 和**adStateOpen** (1)。  
  
## <a name="remarks"></a>备注  
 若要使用[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)常量名，您必须具有在项目中引用 ADO 类型库。 请参阅[使用 ADO 与 ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)有关详细信息。  
  
## <a name="applies-to"></a>适用范围  
 [单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>请参阅  
 [Close 方法 (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Open 方法 (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
