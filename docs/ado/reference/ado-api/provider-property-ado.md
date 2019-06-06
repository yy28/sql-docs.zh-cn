---
title: 提供程序属性 (ADO) |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: a8c571bf143d4aa68fc5785b91929635864e9ce8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702872"
---
# <a name="provider-property-ado"></a>Provider 属性 (ADO)
指示提供程序的名称[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字符串**值，该值指示提供程序名称。  
  
## <a name="remarks"></a>备注  
 使用**提供程序**属性来设置或返回的连接提供程序的名称。 此属性还可以设置的内容[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性或*ConnectionString*自变量[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)方法; 但是，指定提供程序在多个位置而调用**打开**方法可以具有不可预知的结果。 如果不指定任何提供程序，该属性将默认为 MSDASQL ([Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md))。  
  
 **提供程序**时该连接已关闭，只读方式打开时，属性为读/写。 该设置才会生效之前，或者打开**连接**对象或访问[属性](../../../ado/reference/ado-api/properties-collection-ado.md)的集合**连接**对象。 如果该设置不是有效的就会出错。  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Provider 和 DefaultDatabase 属性示例 (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Provider 和 DefaultDatabase 属性示例 (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)   
 [附录 A：提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)
