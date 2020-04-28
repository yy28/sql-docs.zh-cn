---
title: State 属性（ADO MD） |Microsoft Docs
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
ms.openlocfilehash: 0c11bb74b62d54b1e2489cba5dd7cd35ee376a41
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67949156"
---
# <a name="state-property-ado-md"></a>State 属性 (ADO MD)
指示单元集的当前状态。  
  
## <a name="return-values"></a>返回值  
 返回一个**长**整数，该整数指示[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象的当前条件，并且为只读。 以下值有效： **adStateClosed** （0）和**adStateOpen** （1）。  
  
## <a name="remarks"></a>备注  
 若要使用[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)常量名称，必须在项目中引用 ADO 类型库。 有关详细信息，请参阅将[ADO 与 ADO MD 配合使用](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)。  
  
## <a name="applies-to"></a>应用于  
 [单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [Close 方法（ADO MD）](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Open 方法 (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
