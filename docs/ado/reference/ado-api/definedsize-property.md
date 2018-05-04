---
title: DefinedSize 属性 |Microsoft 文档
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
- Field20::DefinedSize
helpviewer_keywords:
- DefinedSize property [ADO]
ms.assetid: 3ee27314-a305-4fbc-8433-9ee9a909afd6
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b84eb083ba442fc214d63b518c8bab0c001aa229
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="definedsize-property"></a>DefinedSize 属性
指示数据容量[字段](../../../ado/reference/ado-api/field-object.md)对象。  
  
## <a name="return-value"></a>返回值  
 返回**长**值，该值反映定义的大小的一个域，它取决于字段对象的数据类型; 请参阅[类型](../../../ado/reference/ado-api/type-property-ado.md)有关详细信息。 对于使用固定长度的数据类型的字段，返回值是以字节为单位的数据类型的大小。 对于使用可变长度数据类型的字段，这是以下项之一：  
  
1.  以字符为单位的字段的最大长度 (有关**以便您可以排除**和**adVarWChar**) 或以字节为单位 (有关**感**，和**adVarNumeric**) 如果该字段的定义的长度。 例如， **adVarChar(5)** 字段具有的最大长度为 5。  
  
2.  以字符为单位的数据类型的最大长度 (有关**每**和**adWChar**) 或以字节为单位 (有关**adBinary**和**adNumeric**) 如果字段没有定义的长度。  
  
3.  ~ 0 (按位，该值不是 0; 所有位设置为 1) 如果字段和数据类型都不具有定义的最大长度。  
  
4.  对于不具有长度的数据类型，此值设置为 ~ 0 (按位，该值不是 0; 所有位设置为 1)。  
  
## <a name="remarks"></a>注释  
 使用**DefinedSize**属性来确定的数据容量**字段**对象。  
  
 **DefinedSize**和[ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md)所属性不同。 例如，考虑**字段**的声明的类型的对象**以便您可以排除**和**DefinedSize**属性值为 50，包含单个字符。 **ActualSize**它将返回的属性值是单个字符的长度以字节为单位。  
  
## <a name="applies-to"></a>适用范围  
 [字段对象](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另请参阅  
 [ActualSize 和 DefinedSize 属性示例 (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize 和 DefinedSize 属性示例 （VC + +）](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [ActualSize 属性 (ADO)](../../../ado/reference/ado-api/actualsize-property-ado.md)
