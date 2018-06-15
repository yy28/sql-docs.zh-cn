---
title: getCatalog 方法 (SQLServerConnection) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection.getCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e87ef65f-4b5a-4e1c-8db5-7f0932390bb0
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6cc3aedba38d3ade6d08e1829d5970c2585cb1b6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32830502"
---
# <a name="getcatalog-method-sqlserverconnection"></a>getCatalog 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此的当前目录名称[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getCatalog()  
```  
  
## <a name="return-value"></a>返回值  
 A**字符串**，其中包含目录名称。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Connection 接口中的 getCatalog 方法指定此 getCatalog 方法。  
  
 如果未设置，则返回的 SQLServerConnection 对象或为 null 的当前目录属性。 使用显式设置的 catalog 属性[setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md)方法，或通过阅读 TDS 的环境更改为当前目录隐式更新。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
