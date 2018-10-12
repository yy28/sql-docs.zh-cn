---
title: getCatalog 方法 (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e87ef65f-4b5a-4e1c-8db5-7f0932390bb0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 04be6bfd2e90c63476ce671ce8e12e1103184f4d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47691877"
---
# <a name="getcatalog-method-sqlserverconnection"></a>getCatalog 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 对象的当前目录名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getCatalog()  
```  
  
## <a name="return-value"></a>返回值  
 一个包含目录名称的字符串。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getCatalog 方法由 java.sql.Connection 接口中的 getCatalog 方法指定。  
  
 如果未设置，则返回 SQLServerConnection 对象，则为 null 的当前目录属性。 使用 [setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md) 方法显式设置目录属性，或者可通过读取当前目录的 TDS 环境更改隐式更新目录属性。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
