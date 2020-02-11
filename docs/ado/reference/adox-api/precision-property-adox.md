---
title: Precision 属性（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::put_Precision
- _Column::PutPrecision
- _Column::GetPrecision
- _Column::get_Precision
- _Column::Precision
helpviewer_keywords:
- Precision property [ADOX]
ms.assetid: 0e0ecbbf-d7de-49d4-a128-5a519ecd54ba
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d1416842f3c122e9e5e5e28b8a14310b679697cd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67965565"
---
# <a name="precision-property-adox"></a>Precision 属性 (ADOX)
指示[列](../../../ado/reference/adox-api/column-object-adox.md)中数据值的最大精度。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置并返回一个**Long**值，该值为[类型](../../../ado/reference/adox-api/type-property-column-adox.md)属性为数值类型时列中数据值的最大精度。 对于所有其他数据类型，将忽略**精度**。  
  
## <a name="remarks"></a>备注  
 默认值为零 (**0**)。  
  
 对于已追加到集合的[列](../../../ado/reference/adox-api/column-object-adox.md)对象，此属性是只读的。  
  
## <a name="applies-to"></a>应用于  
 [列对象 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [ADOX 代码示例： NumericScale 和 Precision 属性示例（VB）](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Type 属性（列）（ADOX）](../../../ado/reference/adox-api/type-property-column-adox.md)   
 [列对象 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
