---
title: Name 属性 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Name
- Field20::Name
helpviewer_keywords:
- Name property [ADO]
ms.assetid: cfd0e29c-8310-44ab-85c3-5761184b865d
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 834a04e01587be21938d461ac1645802bad624d0
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35279576"
---
# <a name="name-property-ado"></a>Name 属性 (ADO)
指示对象的名称。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字符串**值，该值指示对象的名称。  
  
## <a name="remarks"></a>Remarks  
 使用**名称**属性分配一个名称或检索的名称**命令**，**属性**，**字段**，或**参数**对象。  
  
 值为读/写上**命令**对象和在只读**属性**对象。  
  
 有关**字段**对象，**名称**是通常是只读的。 但是，新对于**字段**已追加到的对象[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合[记录](../../../ado/reference/ado-api/record-object-ado.md)，**名称**是读/写之后才[值](../../../ado/reference/ado-api/value-property-ado.md)属性**字段**已指定的数据提供程序已经成功地添加新和**字段**通过调用[更新](../../../ado/reference/ado-api/update-method.md)方法**字段**集合。  
  
 有关**参数**对象尚未附加到[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合，**名称**属性为读/写。 为追加**参数**对象和所有其他对象，**名称**属性是只读的。 不必在集合中是唯一名称。  
  
 你可以检索**名称**按序号引用，此后可以按名称直接引用对象的对象属性。 例如，如果`rstMain.Properties(20).Name`产生`Updatability`，您随后可以参考此属性作为`rstMain.Properties("Updatability")`。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[字段对象](../../../ado/reference/ado-api/field-object.md)|  
|[参数对象](../../../ado/reference/ado-api/parameter-object.md)|[属性对象 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>请参阅  
 [特性和名称属性示例 (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [特性和名称属性示例 （VC + +）](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
