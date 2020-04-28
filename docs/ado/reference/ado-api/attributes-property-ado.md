---
title: Attributes 属性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Attributes
- Field20::Attributes
- _Parameter::Attributes
helpviewer_keywords:
- Attributes property [ADO]
ms.assetid: acc15d40-68a6-4ba9-85bd-12d331aecaa6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b40b71dee32608756721d84a2e13f5f54f7bcbfa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67920546"
---
# <a name="attributes-property-ado"></a>Attributes 属性 (ADO)
指示对象的一个或多个特征。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个**长整型**值。  
  
 对于[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象，"**属性**" 属性是 "读/写"，其值可以是一个或多个[XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md)值的总和。 默认值为零 (0)。  
  
 对于[参数](../../../ado/reference/ado-api/parameter-object.md)对象，"**属性**" 属性是 "读/写"，其值可以是任何一个或多个[ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md)值的总和。 默认值为**adParamSigned**。  
  
 对于[字段](../../../ado/reference/ado-api/field-object.md)对象，"**属性**" 属性可以是一个或多个[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)值的总和。 它通常是只读的。 但是，对于已附加到[记录](../../../ado/reference/ado-api/record-object-ado.md)的[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合的新**字段**对象，仅在指定了**字段**的[值](../../../ado/reference/ado-api/value-property-ado.md)属性并且数据访问接口已成功添加新**字段**之后，**属性**才是可读/**写的。** [Update](../../../ado/reference/ado-api/update-method.md)  
  
 对于[属性](../../../ado/reference/ado-api/property-object-ado.md)对象，"**属性**" 属性是只读的，它的值可以是任何一个或多个[PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md)值的总和。  
  
## <a name="remarks"></a>备注  
 使用 "**属性**" 属性可设置或返回**连接**对象、**参数**对象、**字段**对象或**属性**对象的特征。  
  
 设置多个属性时，可以对相应的常量求和。 如果将属性值设置为包含不兼容常量的总和，则会发生错误。  
  
> [!NOTE]
>  **远程数据服务使用情况**此属性在客户端**连接**对象上不可用。  
  
## <a name="applies-to"></a>应用于  
  
|||  
|-|-|  
|[连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[字段对象](../../../ado/reference/ado-api/field-object.md)|  
|[参数对象](../../../ado/reference/ado-api/parameter-object.md)|[属性对象 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>另请参阅  
 [特性和名称属性示例（VB）](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [特性和名称属性示例（VC + +）](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
 [AppendChunk 方法（ADO）](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [BeginTrans、CommitTrans 和 RollbackTrans 方法（ADO）](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [GetChunk 方法 (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
