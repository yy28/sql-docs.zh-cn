---
title: "Attributes 属性 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::Attributes
- Field20::Attributes
- _Parameter::Attributes
helpviewer_keywords:
- Attributes property [ADO]
ms.assetid: acc15d40-68a6-4ba9-85bd-12d331aecaa6
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9bffe5215cbb93e24f6914d6d56a349c9d35f6b7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="attributes-property-ado"></a>Attributes 属性 (ADO)
指示一个或多个特征的对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**长**值。  
  
 有关[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象，**属性**属性为读/写，并且其值可以是一个或多个总和[XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md)值。 默认值为零 (0)。  
  
 有关[参数](../../../ado/reference/ado-api/parameter-object.md)对象，**属性**属性为读/写，并且其值可以是任何一个或多个总和[ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md)值。 默认值是**adParamSigned**。  
  
 有关[字段](../../../ado/reference/ado-api/field-object.md)对象，**属性**属性可以是一个或多个总和[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)值。 它是通常是只读的。 但是，新对于**字段**已追加到的对象[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合[记录](../../../ado/reference/ado-api/record-object-ado.md)，**属性**为仅读/写后[值](../../../ado/reference/ado-api/value-property-ado.md)属性**字段**已指定和新**字段**已成功添加数据提供程序通过调用[更新](../../../ado/reference/ado-api/update-method.md)方法**字段**集合。  
  
 有关[属性](../../../ado/reference/ado-api/property-object-ado.md)对象，**属性**属性是只读的且其值可以是任何一个或多个总和[PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md)值。  
  
## <a name="remarks"></a>注释  
 使用**属性**属性来设置或返回的特征**连接**对象，**参数**对象，**字段**对象，或**属性**对象。  
  
 当你设置多个属性时，你可以总和的相应常量。 如果属性值设置为包括不兼容的常量的总和中时，出现错误。  
  
> [!NOTE]
>  **远程数据服务使用情况**此属性不是可在客户端上**连接**对象。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[字段对象](../../../ado/reference/ado-api/field-object.md)|  
|[参数对象](../../../ado/reference/ado-api/parameter-object.md)|[属性对象 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>另请参阅  
 [特性和名称属性示例 (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [特性和名称属性示例 （VC + +）](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
 [AppendChunk 方法 (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [BeginTrans、 CommitTrans 和不方法 (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [GetChunk 方法 (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)

