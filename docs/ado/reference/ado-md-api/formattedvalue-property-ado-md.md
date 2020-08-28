---
description: FormattedValue 属性 (ADO MD)
title: FormattedValue 属性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 5905b4aba040505c60fa78721718b3ab03c51622
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986698"
---
# <a name="formattedvalue-property-ado-md"></a>FormattedValue 属性 (ADO MD)
指示 [单元格值](./cell-object-ado-md.md) 的格式化显示。  
  
## <a name="return-values"></a>返回值  
 返回一个 **字符串** ，并且为只读。  
  
## <a name="remarks"></a>注解  
 使用**FormattedValue**属性可获取[单元](./cell-object-ado-md.md)对象的[value](./value-property-ado-md.md)属性的格式化显示值。 例如，如果单元格的值为1056.87，此值表示美元金额，则 **FormattedValue** 将为 $1056.87。  
  
## <a name="applies-to"></a>适用于  
 [单元对象 (ADO MD)](./cell-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [ (VB) 单元集示例 ](./cellset-example-vb.md)   
 [Value 属性 (ADO MD)](./value-property-ado-md.md)