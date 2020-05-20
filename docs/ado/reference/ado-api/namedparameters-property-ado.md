---
title: NamedParameters 属性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::NamedParameters
helpviewer_keywords:
- NamedParameters property [ADO]
ms.assetid: 42409387-026c-435f-a9b1-bf4167095875
author: rothja
ms.author: jroth
ms.openlocfilehash: 432a4968a301e51c1ca69e3b84ea80e0a19e32bb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762408"
---
# <a name="namedparameters-property-ado"></a>NamedParameters 属性 (ADO)
指示是否应将参数名称传递给提供程序。  
  
## <a name="remarks"></a>备注  
 当此属性为 true 时，ADO 将为[命令对象](../../../ado/reference/ado-api/command-object-ado.md)传递**参数**集合中每个参数的**Name**属性的值。 提供程序使用参数名来匹配**CommandText**或**CommandStream**属性中的参数。 如果此属性为 false （默认值），则忽略参数名，并且提供程序使用参数的顺序将值与**CommandText**或**CommandStream**属性中的参数相匹配。  
  
## <a name="applies-to"></a>应用于  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [CommandText 属性（ADO）](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandStream 属性（ADO）](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [参数集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
