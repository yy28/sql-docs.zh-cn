---
title: DefinedSize 属性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::DefinedSize
helpviewer_keywords:
- DefinedSize property [ADO]
ms.assetid: 3ee27314-a305-4fbc-8433-9ee9a909afd6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4267776593637a01aef38a218f7272261fd1d448
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63140175"
---
# <a name="definedsize-property"></a>DefinedSize 属性
指示数据容量[字段](../../../ado/reference/ado-api/field-object.md)对象。  
  
## <a name="return-value"></a>返回值  
 返回**长**值，该值反映的定义的大小的一个字段，这取决于字段对象的数据类型; 请参阅[类型](../../../ado/reference/ado-api/type-property-ado.md)有关详细信息。 对于使用固定长度的数据类型的字段，返回值是以字节为单位的数据类型的大小。 对于使用可变长度数据类型的字段，这是以下值之一：  
  
1.  中字符的字段的最大长度 (对于**adVarChar**和**adVarWChar**) 或以字节为单位 (有关**adVarBinary**，和**adVarNumeric**) 如果该字段具有定义的长度。 例如， **adVarChar(5)** 字段具有最大长度为 5。  
  
2.  以字符为单位的数据类型的最大长度 (对于**每**和**adWChar**) 或以字节为单位 (对于**adBinary**并**adNumeric**) 如果字段不具有定义的长度。  
  
3.  ~ 0 (按位，值不是 0; 所有位设置为 1) 如果该字段和数据类型都不具有定义的最大长度。  
  
4.  对于不具有长度的数据类型，此值设置为 ~ 0 (按位，值不是 0; 所有位设置为 1)。  
  
## <a name="remarks"></a>备注  
 使用**DefinedSize**属性来确定的数据容量**字段**对象。  
  
 **DefinedSize**并[ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md)属性的不同。 例如，考虑**字段**对象的声明的类型**adVarChar**和一个**DefinedSize**属性值为 50，包含单个字符。 **ActualSize**它将返回的属性值是单个字符的长度以字节为单位。  
  
## <a name="applies-to"></a>适用范围  
 [字段对象](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>请参阅  
 [ActualSize 和 DefinedSize 属性示例 (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize 和 DefinedSize 属性示例 （VC + +）](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [ActualSize 属性 (ADO)](../../../ado/reference/ado-api/actualsize-property-ado.md)
