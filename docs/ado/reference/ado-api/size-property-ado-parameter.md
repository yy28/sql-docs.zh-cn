---
title: "Size 属性 （ADO 参数） |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: _Parameter::Size
helpviewer_keywords: Size property [ADO Parameter]
ms.assetid: e6bad449-ebdb-4dd3-886a-9e6f1e7ee5d2
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b0c9454da339650414e9ecce6826907240e2cc53
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="size-property-ado-parameter"></a>Size 属性 （ADO 参数）
指示的最大大小，以字节或字符，[参数](../../../ado/reference/ado-api/parameter-object.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**长**值，该值指示字节或字符中的值的最大大小**参数**对象。  
  
## <a name="remarks"></a>Remarks  
 使用**大小**属性，以确定值写入到的最大大小，或从读取[值](../../../ado/reference/ado-api/value-property-ado.md)属性**参数**对象。  
  
 如果你指定的可变长度数据类型**参数**对象 (例如，任何**字符串**类型，如**以便您可以排除**)，你必须设置对象的**大小**之前追加到属性[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合; 否则，将会出错。  
  
 如果你已具有追加**参数**对象传递给**参数**集合[命令](../../../ado/reference/ado-api/command-object-ado.md)对象，并将其类型更改为可变长度数据类型，则必须设置**参数**对象的**大小**属性在执行之前**命令**对象; 否则，将会出错。  
  
 如果你使用[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)方法来获取参数信息来自提供程序和它返回一个或多个可变长度数据类型**参数**对象，ADO 可能会基于的参数分配内存其最大的潜在大小，这会导致在执行期间出错。 若要防止出现错误，应显式设置**大小**执行命令之前这些参数的属性。  
  
 **大小**属性为读/写。  
  
## <a name="applies-to"></a>适用范围  
 [参数对象](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>另请参阅  
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 （VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Size 属性（ADO 流）](../../../ado/reference/ado-api/size-property-ado-stream.md)
