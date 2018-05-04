---
title: setClientInfo 方法 (java.util.Properties) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b2a8ec0b-40a2-44d1-90d9-a810d4132e56
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0785a1ee2c2aa96f6058e0dba2296af524cd345e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="setclientinfo-method-javautilproperties"></a>setClientInfo 方法 (java.util.Properties)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置连接的客户端信息属性的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setClientInfo (java.util.Properties properties)  
```  
  
#### <a name="parameters"></a>Parameters  
 *属性*  
  
 一个包含客户端信息属性设置的列表的属性对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Connection 接口中的 setClientInfo 方法指定此 setClientInfo 方法。  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]不支持任何客户端信息属性。 如果此方法将生成警告*属性*输入的参数不是指一个空的属性集。 也就是说，此方法针对应用程序要设置的属性生成警告。 应用程序应使用[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md)方法[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)类检索每个警告。  
  
## <a name="see-also"></a>另请参阅  
 [setClientInfo 方法&#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
