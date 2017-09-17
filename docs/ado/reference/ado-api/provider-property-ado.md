---
title: "提供程序属性 (ADO) |Microsoft 文档"
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
- Connection15::get_Provider
- Connection15::PutProvider
- Connection15::put_Provider
- Connection15::GetProvider
- Connection15::Provider
helpviewer_keywords:
- Provider property [ADO]
ms.assetid: 0ff70e72-0061-4ffc-90fb-e3ea23129bb2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1839d8bc9c954d3f5ceeafca2b604304801f643f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="provider-property-ado"></a>提供程序属性 (ADO)
指示提供程序名称[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字符串**值，该值指示提供程序名称。  
  
## <a name="remarks"></a>注释  
 使用**提供程序**属性来设置或返回提供程序的连接的名称。 此属性还可以设置的内容[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性或*ConnectionString*参数[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)方法; 但是，指定提供程序在多个位置时调用**打开**方法都有不可预知的结果。 如果不指定任何提供程序，则该属性将默认为 MSDASQL ([Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md))。  
  
 **提供程序**属性为读/写，当连接已关闭，并且只读打开时。 该设置将不会生效之前你任一打开**连接**对象或访问[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合**连接**对象。 如果设置不是有效的就会出错。  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [提供程序和 DefaultDatabase 属性示例 (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [提供程序和 DefaultDatabase 属性示例 (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)   
 [附录 a： 提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)

