---
title: Provider 属性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fae46773befb13105ed9dcd81b1116be48cf0675
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931450"
---
# <a name="provider-property-ado"></a>Provider 属性 (ADO)
指示[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象的访问接口的名称。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个指示提供程序名称的**字符串**值。  
  
## <a name="remarks"></a>备注  
 使用**provider**属性可设置或返回连接的访问接口的名称。 此属性还可以通过[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性的内容或[Open](../../../ado/reference/ado-api/open-method-ado-connection.md)方法的*connectionstring*参数设置;但是，在调用**Open**方法时在多个位置指定提供程序可能会产生不可预知的结果。 如果未指定提供程序，则该属性将默认为 MSDASQL （[Microsoft OLE DB ODBC 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)）。  
  
 当连接关闭并且处于打开状态时，**提供程序**属性是可读/写的。 只有打开**连接**对象或访问**连接**对象的[Properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合后，此设置才会生效。 如果设置无效，则会发生错误。  
  
## <a name="applies-to"></a>应用于  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [Provider 和 DefaultDatabase 属性示例（VB）](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Provider 和 DefaultDatabase 属性示例（VB）](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [适用于 ODBC 的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)   
 [附录 A：提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)
