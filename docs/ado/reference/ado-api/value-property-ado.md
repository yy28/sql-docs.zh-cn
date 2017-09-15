---
title: "值属性 (ADO) |Microsoft 文档"
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
- Field20::Value
- _Parameter::Value
helpviewer_keywords:
- Value property [ADO]
ms.assetid: 48919c74-86d4-462e-99b9-8854ceb8d683
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 17e3c9f28e42dbd70118bb29a330514a9c29e013
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="value-property-ado"></a>值属性 (ADO)
指示分配给值[字段](../../../ado/reference/ado-api/field-object.md)，[参数](../../../ado/reference/ado-api/parameter-object.md)，或[属性](../../../ado/reference/ado-api/property-object-ado.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**Variant**值，该值指示对象的值。 默认值取决于[类型](../../../ado/reference/ado-api/type-property-ado.md)属性。  
  
## <a name="remarks"></a>注释  
 使用**值**属性来设置或返回数据自**字段**对象，设置或返回参数值和**参数**对象，或用于设置或返回与属性设置**属性**对象。 是否**值**属性为读/写或只读取决于多种因素，??? 请参阅各自对象主题以了解更多信息。  
  
 ADO 允许设置和返回长度的二进制数据与**值**属性。  
  
> [!NOTE]
>  有关**参数**对象、 ADO 读取**值**属性一次从提供程序。 如果命令包含**参数**其**值**属性为空，并且你创建[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)从该命令，请确保先关闭**记录集**之前检索**值**属性。 否则为对于某些提供程序，**值**属性可能为空，并且不会包含正确的值。  
>   
>  新**字段**已追加到的对象[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合[记录](../../../ado/reference/ado-api/record-object-ado.md)对象，**值**属性必须设置在任何其他之前**字段**可以指定属性。 首先，为特定值**值**属性必须具有已分配和[更新](../../../ado/reference/ado-api/update-method.md)上**字段**名集合。 然后，其他属性，如[类型](../../../ado/reference/ado-api/type-property-ado.md)或[属性](../../../ado/reference/ado-api/attributes-property-ado.md)可访问。  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[字段对象](../../../ado/reference/ado-api/field-object.md)|[参数对象](../../../ado/reference/ado-api/parameter-object.md)|[属性对象 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>另请参阅  
 [值属性示例 (VB)](../../../ado/reference/ado-api/value-property-example-vb.md)   
 [值属性示例 （VC + +）](../../../ado/reference/ado-api/value-property-example-vc.md)   

