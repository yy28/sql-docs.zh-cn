---
title: FormattedValue 属性（ADO MD） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell::FormattedValue
- FormattedValue
helpviewer_keywords:
- FormattedValue property [ADO MD]
ms.assetid: 5c06451e-06ec-4da6-9a87-2d043469248a
author: rothja
ms.author: jroth
ms.openlocfilehash: 1acc577b1822beb69826120034ffa4872e60c60b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764238"
---
# <a name="formattedvalue-property-ado-md"></a>FormattedValue 属性 (ADO MD)
指示[单元格值](../../../ado/reference/ado-md-api/cell-object-ado-md.md)的格式化显示。  
  
## <a name="return-values"></a>返回值  
 返回一个**字符串**，并且为只读。  
  
## <a name="remarks"></a>备注  
 使用**FormattedValue**属性可获取[单元](../../../ado/reference/ado-md-api/cell-object-ado-md.md)对象的[value](../../../ado/reference/ado-md-api/value-property-ado-md.md)属性的格式化显示值。 例如，如果单元格的值为1056.87，此值表示美元金额，则**FormattedValue**将为 $1056.87。  
  
## <a name="applies-to"></a>应用于  
 [单元对象 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [单元集示例（VB）](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Value 属性 (ADO MD)](../../../ado/reference/ado-md-api/value-property-ado-md.md)
