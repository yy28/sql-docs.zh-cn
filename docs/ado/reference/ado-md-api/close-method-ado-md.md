---
title: Close 方法 (ADO MD) |Microsoft 文档
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
- Close
- Cellset::Close
helpviewer_keywords:
- Close method [ADO MD]
ms.assetid: a3aa594d-f9d4-4654-8625-ec20153ff5d9
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 03cf786407d12e4ff38ae7a58cedcb110af1734d
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="close-method-ado-md"></a>Close 方法 (ADO MD)
关闭打开的单元集。  
  
## <a name="syntax"></a>语法  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>注释  
 使用**关闭**方法来关闭[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象将释放关联的数据，包括中任何相关的数据[单元格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)，[轴](../../../ado/reference/ado-md-api/axis-object-ado-md.md)，[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)，或[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)对象。 关闭**单元集**不会删除它从内存中; 你可以更改其属性设置，以后再打开它。 若要完全消除从内存的对象，请将对象变量设置为**执行任何操作**。  
  
 你可以稍后调用[打开](../../../ado/reference/ado-md-api/open-method-ado-md.md)方法重新打开**单元集**使用相同或另一个源字符串。 虽然**单元集**对象已关闭，检索任何属性或调用引用基础数据的任何方法或元数据生成一个错误。  
  
## <a name="applies-to"></a>适用范围  
 [单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [轴对象 (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [单元格对象 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [成员对象 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)   
 [Open 方法 (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)   
 [位置对象 (ADO MD)](../../../ado/reference/ado-md-api/position-object-ado-md.md)   
 [State 属性 (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
