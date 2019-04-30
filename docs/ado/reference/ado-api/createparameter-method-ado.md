---
title: CreateParameter 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::raw_CreateParameter
- Command15::CreateParameter
helpviewer_keywords:
- CreateParameter method [RDS]
ms.assetid: 9666fdcc-0544-4ed7-a97b-c415f2a56d7e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b150fe1c0c7260960140558eeff74b54c0798d80
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63308618"
---
# <a name="createparameter-method-ado"></a>CreateParameter 方法 (ADO)
创建一个新[参数](../../../ado/reference/ado-api/parameter-object.md)对象使用指定的属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set parameter = command.CreateParameter (Name, Type, Direction, Size, Value)  
```  
  
## <a name="return-value"></a>返回值  
 返回**参数**对象。  
  
#### <a name="parameters"></a>Parameters  
 *名称*  
 可选。 一个**字符串**值，该值包含的名称**参数**对象。  
  
 *类型*  
 可选。 一个[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)值，该值指定的数据类型**参数**对象。  
  
 *方向*  
 可选。 一个[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)值，该值指定的类型**参数**对象。  
  
 *大小*  
 可选。 一个**长**值，该值以字节或字符指定参数值的最大长度。  
  
 *ReplTest1*  
 可选。 一个**Variant**指定的值**参数**对象。  
  
## <a name="remarks"></a>备注  
 使用**CreateParameter**方法来创建一个新**参数**具有指定的名称、 类型、 方向、 大小和值对象。 在参数中传递的任何值写入到的相应**参数**属性。  
  
 此方法不会自动追加**参数**对象传递给**参数**的集合[命令](../../../ado/reference/ado-api/command-object-ado.md)对象。 这允许您设置其他属性时将追加将验证其值 ADO**参数**到集合的对象。  
  
 如果指定中的可变长度数据类型*类型*自变量，您必须将传递*大小*参数或一组[大小](../../../ado/reference/ado-api/size-property-ado-parameter.md)属性**参数**对象之前将向其追加**参数**集合; 否则，就会出错。  
  
 如果指定的数值数据类型 (**adNumeric**或**adDecimal**) 中*类型*参数，则您还必须设置[NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)和[精度](../../../ado/reference/ado-api/precision-property-ado.md)属性。  
  
## <a name="applies-to"></a>适用范围  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Append 和 CreateParameter 方法示例 (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Append 和 CreateParameter 方法示例 （VC + +）](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [参数对象](../../../ado/reference/ado-api/parameter-object.md)   
 [参数集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
