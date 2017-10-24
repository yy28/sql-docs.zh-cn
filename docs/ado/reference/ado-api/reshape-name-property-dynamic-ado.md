---
title: "重新调整形状名称属性的动态 (ADO) |Microsoft 文档"
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
helpviewer_keywords:
- Reshape Name property [ADO]
ms.assetid: 690229d1-46cc-42e6-a57d-4438251fe248
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3b14593e427db76994976091e5916ffe49aefe82
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="reshape-name-property-dynamic-ado"></a>重新调整形状名称属性的动态 (ADO)
指定的名称[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
## <a name="return-values"></a>返回值  
 返回**字符串**值的名称**记录集**。  
  
## <a name="remarks"></a>注释  
 名称的连接或直到持续期间保留**记录集**已关闭。  
  
 **重新调整形状名称**属性主要用于与的重新调整功能一起使用[用于 OLE DB 的 Microsoft 数据调整服务](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)服务提供程序。 名称必须是唯一的以参与重新调整。  
  
 此属性是只读的但是，可以设置间接时**记录集**创建。 例如，如果的子句形状命令将创建**记录集**并为其提供通过使用别名**AS**别名关键字，分配给**重新调整形状名称**属性。 如果声明没有别名，则**重新调整形状名称**属性分配一个唯一的名称生成的调整服务的数据。 别名名称是否与现有名称相同**记录集**，既不**记录集**可以被重新整形，直到其中一个被释放。 可以通过设置中唯一的名称更改默认行为[重新调整形状名称](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)的 ADO 连接上的属性**True**。 设置此属性使调整更改分配的用户名称，如有必要，以确保唯一性服务权限的数据。 有关重新调整的详细信息，请参阅[用于 OLE DB （ADO 服务提供程序） 的 Microsoft 数据调整服务](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)。  
  
 使用**重新调整形状名称**当你想要引用时，属性**记录集**在形状命令中，或你不知道名称，因为它已由数据调整服务生成。 在这种情况下，无法通过串联解决返回的字符串的命令生成形状命令**重新调整形状名称**属性。  
  
 **重新调整形状名称**动态属性追加到**记录集**对象的[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合时[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [调整用于 OLE DB （ADO 服务提供程序） 的服务的 Microsoft 数据](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)   
 [在常规的形状命令](../../../ado/guide/data/shape-commands-in-general.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

