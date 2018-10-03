---
title: Reshape Name 属性-动态 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Reshape Name property [ADO]
ms.assetid: 690229d1-46cc-42e6-a57d-4438251fe248
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6a07ec878b1198fbf23bfb251460d83869313c83
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696822"
---
# <a name="reshape-name-property-dynamic-ado"></a>Reshape Name 属性 - 动态 (ADO)
指定的名称[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
## <a name="return-values"></a>返回值  
 返回**字符串**，它是值的名称**记录集**。  
  
## <a name="remarks"></a>备注  
 名称保持不变的持续时间的连接或直到**记录集**已关闭。  
  
 **改变形状名称**属性主要用于与的重新调整功能一起使用[适用于 OLE DB 的 Microsoft Data Shaping 服务](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)服务提供程序。 名称必须是唯一的以参与重新定型。  
  
 此属性是只读的但可以设置间接时**记录集**创建。 例如，如果一个子句的形状命令将创建**记录集**并为其提供通过使用别名**AS**关键字，该别名分配给**重新调整形状名称**属性。 如果声明没有别名，则**改变形状名称**属性分配生成的数据整理服务的唯一名称。 别名名称是否与现有的同名**记录集**，既不**记录集**直到其中一个发布可以解答。 可以通过设置唯一的名称中更改默认行为[改变形状名称](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)ADO 连接上的属性**True**。 将此属性设置为提供数据整理服务的权限来更改分配的用户名称，如有必要，以确保唯一性。 有关重新调整的详细信息，请参阅[适用于 OLE DB （ADO 服务提供商） 的 Microsoft Data Shaping 服务](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)。  
  
 使用**改变形状名称**属性时想要引用**记录集**形状命令时，或您不知道名称，因为它已由 Data Shaping 服务生成。 在这种情况下，无法生成形状命令通过串联命令返回的字符串周围**改变形状名称**属性。  
  
 **重新调整形状名称**动态属性追加到**记录集**对象的[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合时[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Microsoft 数据整理服务用于 OLE DB （ADO 服务提供程序）](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)   
 [常用 shape 命令](../../../ado/guide/data/shape-commands-in-general.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
