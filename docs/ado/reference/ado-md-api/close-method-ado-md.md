---
title: Close 方法 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Close
- Cellset::Close
helpviewer_keywords:
- Close method [ADO MD]
ms.assetid: a3aa594d-f9d4-4654-8625-ec20153ff5d9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4f01845752c0ee1f9187ea3d209a97509f87a5a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66709574"
---
# <a name="close-method-ado-md"></a>Close 方法 (ADO MD)
关闭打开的单元集。  
  
## <a name="syntax"></a>语法  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>备注  
 使用**关闭**方法以关闭[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象将释放关联的数据，包括任何相关数据[单元格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)，[轴](../../../ado/reference/ado-md-api/axis-object-ado-md.md)，[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)，或[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)对象。 关闭**单元集**不会删除从内存; 可以更改其属性设置，以后再打开它。 若要完全消除从内存对象，请将对象变量设置为**Nothing**。  
  
 稍后可以调用[开放](../../../ado/reference/ado-md-api/open-method-ado-md.md)方法以重新打开**单元集**使用相同或另一个源字符串。 虽然**单元集**对象已关闭，检索的任何属性或调用任何方法的引用的基础数据或元数据生成一个错误。  
  
## <a name="applies-to"></a>适用范围  
 [单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>请参阅  
 [轴对象 (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Cell 对象 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [成员对象 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)   
 [Open 方法 (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)   
 [位置对象 (ADO MD)](../../../ado/reference/ado-md-api/position-object-ado-md.md)   
 [State 属性 (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
