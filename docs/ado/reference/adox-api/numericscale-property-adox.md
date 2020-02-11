---
title: NumericScale 属性（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::PutNumericScale
- _Column::GetNumericScale
- _Column::NumericScale
- _Column::put_NumericScale
- _Column::get_NumericScale
helpviewer_keywords:
- NumericScale property [ADOX]
ms.assetid: 573ee5d1-57c7-4a27-be79-a0e12944ad9b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 16fdefcb06d2b1b90dfc3da39aaf6b1c9659debc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67965745"
---
# <a name="numericscale-property-adox"></a>NumericScale 属性 (ADOX)
指示列中数值的小数位数。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置并返回一个**字节**值，该值表示当[类型](../../../ado/reference/adox-api/type-property-column-adox.md)属性为**adNumeric**或**adDecimal**时，列中的数据值的小数位数。 对于所有其他数据类型，将忽略**NumericScale** 。  
  
## <a name="remarks"></a>备注  
 默认值为零 (0)。  
  
 对于已追加到集合的[列](../../../ado/reference/adox-api/column-object-adox.md)对象， **NumericScale**为只读。  
  
## <a name="applies-to"></a>应用于  
 [列对象 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [ADOX 代码示例： NumericScale 和 Precision 属性示例（VB）](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Type 属性（列）(ADOX)](../../../ado/reference/adox-api/type-property-column-adox.md)
